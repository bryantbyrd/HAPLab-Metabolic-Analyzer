# Example recordings (synthetic)

These three files are **invented data**. Every value is computed by `tools/make_synthetic_examples.py`
from a simple model with a fixed random seed. No athlete, student or laboratory record was used,
copied or altered to make them. They are in the layout of a Parvo TrueOne 2400 "Metabolic Text
Report" export, which is the format the app imports.

| File | What it imitates |
|---|---|
| `synthetic_cycling_step_test_PRE.csv` | Cycling step test, 3-min stages from 100 to 300 W, blood lactate at the end of each stage |
| `synthetic_cycling_step_test_POST.csv` | The same invented rider "after training", 100 to 325 W — for the comparison view |
| `synthetic_treadmill_step_test.csv` | Treadmill step test, 3-min stages from 6.0 to 10.8 mph, blood lactate at the end of each stage |

## Try them

1. Open the app and choose `synthetic_cycling_step_test_PRE.csv` under **Import test data**.
2. Confirm the stages the app proposes. Charts, ventilatory thresholds, lactate thresholds, the
   substrate table and the Metabolic Response Map are then filled.
3. To compare two tests: open the POST file first and use **Save** to keep its session file. Then
   open the PRE file and choose that session file with **Load Comparison**.

Because the data are invented, the thresholds and zones they produce describe the model, not a person.
Do not use them as reference values.
