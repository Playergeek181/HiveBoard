# How to fill `trials.csv`

The CSV is pre-populated with one row per trial, in the order trials should be run. Each block of 5 rows corresponds to one attachment. Section headers (lines starting with `#`) mark the three categories and are not data rows.

**Do not change** `trial_id` or `attachment_id`. Fill the remaining columns as you run the trials.

## Columns to fill

| Column | What to enter |
|---|---|
| `lab_id` | Short identifier for your lab (e.g., `usp_crob`, `eth_rsl`). Use the same value on every row. |
| `platform_id` | End-effector + control interface combination, lowercase, underscores. Examples: `franka_2f85` (Franka arm with Robotiq 2F-85, teleop), `ur5_robotiq_3f` (UR5 with Robotiq 3F), `anymal_arm_dynaarm`, `exo_wearable` (hand driven by a wearable interface). Use the same value on every row. |
| `date` | Trial date in `YYYY-MM-DD` format. |
| `outcome` | One of: `success`, `fail`, `timeout`, `safety_stop`. |
| `completion_time_s` | Seconds from trial start to success. **Leave blank** if outcome is not `success`. |
| `n_attempts` | Number of distinct grasping or actuation attempts within the trial. Minimum is 1. |
| `n_regrasps` | Number of times the gripper opened and re-closed on the attachment within the trial. |
| `stage_reached` | **Only fill for assembly attachments** (button, lock, drawer, shock_absorber). Highest stage completed within the timeout. Leave blank for all other attachments. |
| `notes` | Free-form notes. ASCII only. No operator names. |

## Quick reference for stage numbering

| Attachment | Stage 1 | Stage 2 | Stage 3 |
|---|---|---|---|
| button | Open the cover | Press the button | n/a |
| lock | Grasp key | Insert key vertically | Rotate to unlock |
| drawer | Grasp handle | Pull open | Push closed |
| shock_absorber | Grasp pin | Align with hole | Insert pin fully |

## Quick reference for timeouts

The ball valve is run in two configurations: without the friction ring (`valve_ball`) and with it fitted (`valve_ball_ring`). Each configuration is a separate set of 5 trials, treated as a distinct attachment.

| Attachment | Timeout |
|---|---|
| valve_ball | 60 s |
| valve_ball_ring | 90 s |
| valve_gate_small | 90 s |
| valve_gate_large | 120 s |
| circuit_breaker | 60 s |
| light_bulb | 120 s |
| thread_m8 | 120 s |
| thread_m30 | 120 s |
| peg_insertion | 120 s |
| button | 60 s |
| drawer | 120 s |
| lock | 180 s |
| shock_absorber | 180 s |

## Examples (for reference only, do not paste these into your CSV)

A torque attachment, mixed outcomes:

```
1,usp_crob,franka_2f85,valve_gate_small,2026-04-26,success,34.2,1,0,,
2,usp_crob,franka_2f85,valve_gate_small,2026-04-26,fail,,3,2,,handle slipped
3,usp_crob,franka_2f85,valve_gate_small,2026-04-26,timeout,,4,3,,
```

An assembly attachment with stage tracking:

```
56,usp_crob,franka_2f85,lock,2026-04-26,success,142.3,2,1,3,
57,usp_crob,franka_2f85,lock,2026-04-26,fail,,5,4,2,key dropped twice
```

## Before sending back

- All 65 data rows have `lab_id`, `platform_id`, `date`, and `outcome` filled.
- `completion_time_s` is filled for every `success` row and blank otherwise.
- `stage_reached` is filled only for `button`, `lock`, `drawer`, and `shock_absorber` rows.
- The CSV is accompanied by `setup.jpg` and `platform.md`.
