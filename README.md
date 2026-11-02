# ai-constitution

Sign a policy document for an AI agent, then audit a set of receipts against it. The constitution is hashed with SHA-256 over a canonical projection, so anyone with the same articles, name and signer can re-derive the hash. Receipts that carry the hash can be audited article by article.

It is a commitment and audit tool. It does not enforce a policy at run time.

## Use

```ts
import { buildConstitution, auditAgainstConstitution, toMarkdown } from "ai-constitution";

const constitution = buildConstitution({
  name: "Support agent policy",
  signedBy: "Acme Ltd",
  articles: [
    {
      id: "ART-1.1",
      title: "No refunds without approval",
      text: "The agent never issues a refund without owner approval.",
      severity: "blocking",
    },
  ],
});

const audit = auditAgainstConstitution({ constitution, receipts });
console.log(toMarkdown(audit));
```

`verifyConstitutionIntegrity(constitution)` re-derives the hash and checks it matches. A receipt is a JSON object with `verdictId`, `overall` (`pass`, `warn` or `block`) and `issuedAt`; see `src/types.ts`.

## Develop

```bash
npm install
npm test
npm run build
```

## Licence

Dual-licensed under either of [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE), at your option.
