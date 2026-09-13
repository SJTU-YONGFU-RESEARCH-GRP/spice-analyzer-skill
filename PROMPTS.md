# Frozen trial prompt

Paste the analysis prompt into a **new** Cursor chat in the skill repo. Do not paste it into this data repo, and do not paste it into a chat that has already seen another trial.

Do not rerun circuits that already have 10 finished trials (Alfio RAFFC, HoiLee AFFC, Leung NMCF) just because the numbers match. Those runs were independent sessions; agreement is the result. Use this prompt for unfinished netlists, and for a full-suite rerun only if we decide the paper must share one prompt hash.

## Session rules (do these yourself; they are not in the prompt)

The prompt deliberately does not say "trial 7 of 10", "consistency study", or "AnalogGym". Those phrases steer the agent.

1. New chat. Select the same model used for the finished trials (Composer). Do not switch to a thinking model mid-suite.
2. Do not attach, open, or mention any previous `results/` folder, `paper/`, or this file.
3. Copy only the one netlist (and its companion param file, if that circuit has one) into the skill repo. Do not copy other amplifier netlists into the same working folder.
4. After the run finishes, copy the whole `results/<RUN_ID>/` folder here as `results/<RUN_ID>/`. Write `trial_stamp.md` yourself from the stamp below. Do not ask the agent to write the stamp.
5. Record the model name shown in the Cursor model picker. The agent often reports the slug as unknown; the picker label is the one the paper will cite.

## Analysis prompt

Replace the two placeholders. Change nothing else. Do not add a sentence about the paper.

```text
Use the spice-analyzer skill on this netlist only:

<NETLIST_PATH>

Write the full analysis to results/<RUN_ID>/.

Follow the skill defaults. Do not skip PDKs, corners, or Monte Carlo unless the skill itself hard-skips them. Do not use sky130_only, cmos_only, no_corners, or no_mc.

This is a fresh session. Do not read other result folders, other netlists, or any previous report. Analyze only the file above.
```

`<RUN_ID>` is the destination folder name, lowercase, with the trial suffix: `fan_smc_pin_3_trial10`.

## After you move the folder

Create `results/<RUN_ID>/trial_stamp.md` by hand:

```text
run_id: <RUN_ID>
netlist: <filename only>
started: <YYYY-MM-DD local>
host: Cursor
model_picker: <name shown in the model picker>
skill_repo_commit: <git rev-parse HEAD in the skill repo>
new_chat: yes
prior_results_opened: no
prompt: paper/PROMPTS.md analysis prompt
```

If a finished trial has no stamp, do not invent one. The paper will say those trials were fresh chats in the skill repo, with artifacts copied here, and that stamps exist only from this protocol onward.

## Do next (highest value first)

| Netlist file | RUN_ID values still needed |
|--------------|----------------------------|
| Fan_SMC_Pin_3 | `fan_smc_pin_3_trial10` |
| Leung_DFCFC1_Pin_3 | `leung_dfcfc1_pin_3_trial9`, `leung_dfcfc1_pin_3_trial10` |
| Song_DACFC_Pin_3 | trials 6–10 |
| Yan_AZ_Pin_3 | trials 4–10 |
| Tan_CLIA_Pin_3 | trials 3–10 |
| Leung_DFCFC2_Pin_3, Leung_NMCNR_Pin_3, Peng_ACBC_Pin_3, Peng_IAC_Pin_3, Peng_TCFC_Pin_3, Qu2017_AZC_Pin_3, Ramos_PFC_Pin_3, Sau_CFCC_Pin_3 | trials 1–10, only if the four in-progress circuits are at 10 before 2 Oct |

Example, ready to paste:

```text
Use the spice-analyzer skill on this netlist only:

Fan_SMC_Pin_3

Write the full analysis to results/fan_smc_pin_3_trial10/.

Follow the skill defaults. Do not skip PDKs, corners, or Monte Carlo unless the skill itself hard-skips them. Do not use sky130_only, cmos_only, no_corners, or no_mc.

This is a fresh session. Do not read other result folders, other netlists, or any previous report. Analyze only the file above.
```

Use the path the skill repo actually sees if the file is not in the working directory root. The filename in the prompt must be the only circuit identity the agent gets.
