# Requirement Drift Detector

Detect replans that weaken mandatory requirements.

Standalone ES module. No npm install required. Works in **Node.js 20+** and modern browsers (serve over HTTP for browser demos).

## Included files

This repository vendors local dependencies needed by the module:

- `requirement-drift-detector.js` (main)
- `dod-contract.js`

## Install / import

Copy the files into your project, or clone this repository:

```js
import { createContract } from './dod-contract.js';
import { detectDrift } from './requirement-drift-detector.js';
const contract = createContract({id:'invoice', task:'Produce invoice total 42',
  criteria:[{id:'total',description:'JSON total equals 42'}]});
const proposed={...contract,criteria:contract.criteria.map(c=>({...c,mandatory:false}))};
console.log(detectDrift(contract,proposed)); // blocked: true
```

## Use cases

### 1. Stop repairs from weakening the brief

- **Scenario:** A replan makes a failing mandatory invoice criterion optional.
- **Outcome:** Flag the demotion and block the proposed contract change.

### 2. Preserve original constraints

- **Scenario:** A recovery plan quietly removes a no-network constraint.
- **Outcome:** Compare it with the original contract before accepting the plan.

## Exports

- `detectDrift`

## Notes

- Keep API keys and secrets out of this module and out of browser storage.
- Treat verification callbacks, ledger writers, and permission checks as trusted application code.
- This library is intentional local reliability plumbing, not a claim of cryptographic attestation unless stated in the source comments.

## License

MIT
