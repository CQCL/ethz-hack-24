# ethz-hack-24 - Normal forms for $T$ Gate Optimisation
 ETH Quantum Hackathon 2024 with Quantinuum

 Join our slack channel for community discussion and support

 [![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)](https://tketusers.slack.com/join/shared_invite/zt-18qmsamj9-UqQFVdkRzxnXCcKtcarLRA#)


# Update [04/05/24 @ 22:36]


 We’ve been discussing the problem and would like to give you some guidance. Roughly, the steps involved in the implementation are the following

1. Replace each internal Hadamard with a “Hadamard gadget”, introducing the right number of ancillary qubits. Make sure understand well the idea of classically controlled gates

2. Commute the resulting classically controlled Paulis to the end (SEE NOTE BELOW)

3. Rewrite the resulting CNOT+S+T circuit as a phase gadget + CNOT circuit. You can achieve this using the ComposePhasePolyBoxes pass. Find out how to extract the phase polynomial and the CNOT circuit from it, and then replace them with a diagonal gate and a ToffoliBox, to obtain your final normal form. You may find the following links useful:

- [Phase Polynomial overview](https://tket.quantinuum.com/user-manual/manual_circuit.html#phase-polynomials)
- [PhasePolybox docs](https://tket.quantinuum.com/api-docs/circuit.html#pytket.circuit.PhasePolyBox)
- [ComposePhasePolyBoxes docs](https://tket.quantinuum.com/api-docs/passes.html#pytket.passes.ComposePhasePolyBoxes)

## NOTE ON COMMUTATION OF PAULIs

We have re-examined the paper, as well as the original authors’ implementation of the procedure (https://github.com/Luke-Heyfron/TOpt) and it is no longer clear to us how the Pauli commutation used after Hadamard gadgetisation works in the general, non-clifford non-diagonal CNOT+T+S gate set.

We suggest you make the following simplifying assumptions:
- U_f3 has at most one T-gate
- You should gadgetise all Hadamards, however it is sufficient to commute the last Pauli X correction past the last U_f3 block. You DO NOT need to commute any other Pauli X gates. In other words, in the screenshot below, you may leave the first Pauli X gate unchanged and should only commute the second Pauli X gate past U_f3

Alternatively, you can consider the case where all U_fi blocks are diagonal. In this case, commuting the Pauli X gates through to the end should be straightforward.

Bonus: make up your own mind on the feasibility of the procedure described in the paper, and present your arguments tomorrow :)

## Evaluation criteria

The grading tomorrow will be done exclusively by us, and you will only be compared to other teams within our challenge. We do not expect you to have a perfect final solution to this problem, but rather:
 - show us what you have learnt and the journey
 - highlights all your attempts — failed or successful — and explain your approach
 - tell us what you found the most interesting, surprising and what you found particularly challenging.


We wish you a good night and the best of luck for tomorrow!

Luca & Callum




# FIRST: give us your email

-> Fill in [this form](https://forms.office.com/r/MGCB3bTxEm). As soon as we have your email address we will send you an invitation to join the Nexus cloud environment.


# When you are ready to begin

* One member of the team should fork this repository and share the URL with team members. 
* When the challenge begins you will get an email inviting you to set up an account on the Quantinuum Nexus website.
* Follow the instructions on the invite email and visit [https://nexus.quantinuum.com](https://nexus.quantinuum.com). 
* Once you've logged in, click on the burger menu in the top left corner and select 'Lab'.
* Select 'Start' to boot up your hosted workspace.
* Once in the workspace, click on the Git icon in the left-most panel and clone your team's forked repo using the URL from above.
* Run through the Quantinuum Nexus tutorial in [start_here_nexus_tutorial.ipynb](https://github.com/CQCL/ETHZ-HACK-2024/start_here_nexus_tutorial.ipynb) to get started with the Quantinuum Nexus platform.
* Run through the challenge tutorial in [problemsheet.ipynb](https://github.com/CQCL/ETHZ-HACK-2024/problemsheet.ipynb) for the challenge statement and some relevant background.
* When you are ready to submit your project, send a link to your fork of this repository in the slack or with the organisers before the time limit.