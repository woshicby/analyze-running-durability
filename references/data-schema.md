# Durability field-test data schema

Use this reference to request or normalize three or more long-run summaries. Accept spreadsheets, CSV, Markdown tables, screenshots, or prose. Do not require athletes to manufacture missing precision.

## Minimum useful fields

| Field | Meaning | Notes |
|---|---|---|
| `date` | Session date | ISO date preferred |
| `duration_min` | Total moving duration | Record elapsed duration separately if stops matter |
| `first_hr`, `second_hr` | Average heart rate by half | Use comparable sensors and moving segments |
| `first_speed_kmh`, `second_speed_kmh` | Average speed by half | Derive from pace when needed |
| `first_power_w`, `second_power_w` | Average running power by half | Alternative to speed, not required together |
| `rpe_first`, `rpe_second` | RPE by half | State scale, normally 1–10 |
| `carbs_g` | Total carbohydrate during session | Include drink, gels, chews, and food |
| `fluid_ml` | Total fluid during session | Include all drinks |
| `temp_c`, `humidity_pct` | Environmental conditions | Note major changes during the run |
| `elevation_gain_m` | Total climb | Also describe grade profile for trail runs |
| `first_change_min` | Approximate onset of first deterioration | Elapsed minutes from start |
| `first_change_type` | First meaningful change | Use the categories below |
| `recovery_24h`, `recovery_48h` | Recovery notes or rating | Preserve athlete language when useful |

At least one matched output pair is required: speed or power. If neither is available, analyze RPE, symptoms, split times, and recovery qualitatively.

## First-change categories

- `cardiovascular`: heart rate rises relative to output;
- `respiratory`: breathing becomes disproportionately urgent;
- `movement`: cadence, form, coordination, or running power declines;
- `leg_pain`: localized or generalized leg pain, weakness, or impact intolerance;
- `gastrointestinal`: nausea, fullness, cramping, reflux, or inability to eat;
- `cognitive`: attention, navigation, decision quality, or motivation deteriorates;
- `general_fatigue`: no more specific first signal can be identified;
- `other`: retain the athlete's wording.

## Normalization

- Convert pace in `mm:ss/km` to decimal minutes, then calculate `60 / pace_min_per_km`.
- Convert products to carbohydrate grams from nutrition labels. Do not infer grams from “two gels” without product information; report the value as unknown or a range.
- Calculate `carbs_g_h = carbs_g / duration_min * 60`.
- Calculate `fluid_ml_h = fluid_ml / duration_min * 60`.
- Keep sodium separate when provided; do not infer hydration adequacy from fluid volume alone.
- Mark stops, aid-station time, walking, and non-moving time. Decide whether the analysis uses moving or elapsed duration and apply that choice consistently.

## Session design template

Use this compact prompt when information is missing:

> For each of three comparable long runs, send the date, duration, route and climb, temperature and humidity, first- and second-half heart rate plus pace or power, RPE for each half, total carbohydrate grams and fluid milliliters, the first thing that changed and when, and recovery at 24 and 48 hours. Also note stops, sensor problems, illness, pain, or unusual sleep.

## Data quality checks

Flag rather than silently repair:

- heart-rate dropouts, cadence lock, implausible spikes, or different sensor types;
- autopause or long stops that affect halves differently;
- substantial route, surface, altitude, temperature, or humidity differences;
- different footwear when shoe choice could change economy or muscle damage;
- different pre-run nutrition or mid-run carbohydrate availability;
- mismatched duration or intensity;
- a race effort compared with an easy long run;
- trail pace averaged across unlike grades or technical terrain;
- pain, illness, medication, poor sleep, or recent travel.

## Trail and ultra segmentation

Do not compress a variable trail run into one pace–heart-rate number. Prefer repeated segment types:

- runnable flat or gentle grade;
- sustained climb, using grade-adjusted pace, power, vertical speed, or RPE;
- sustained descent, emphasizing speed, cadence, pain, and later performance effects;
- hiking sections;
- periods before and after aid stations;
- daylight versus night when relevant.

Record feet, gastrointestinal tolerance, decision errors, temperature exposure, and aid-station time as part of system durability even when physiological decoupling is unavailable.
