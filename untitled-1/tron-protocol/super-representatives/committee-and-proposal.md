# Committee and Proposal

The committee can modify the TRON network parameters, like transaction fees, block producing reward amount, etc. Committee is composed of the current 27 super representatives. Every super representative has the right to start a proposal. The proposal will be passed after it gets more than 19 approves and will become valid in the next maintenance period.

Only SRs, Partners and Candidates can create a proposal. The network parameters can be modified\(\[min, max\]\). {0,1}: 1 means 'allowed' or 'actived', 0 means no.

Proposal only support YES vote. Since the creation time of the proposal, the proposal is valid within 3 days. If the proposal does not receive enough YES votes within the period of validity, the proposal will be invalid beyond the period of validity. Yes vote can be cancelled.

```text
approveProposal id is_or_not_add_approvalid: proposal id  is_or_not_add_approval: YES vote or cancel YES vote
```

Proposal creator can cancel the proposal before it is passed. Example \(Using wallet-cli\):Shell

