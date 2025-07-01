# OxCal Unordered Phase Model Training Notes
## Roman Cemeteries in England (1st-5th Centuries AD)

## What is a Phase Model?

A **Phase** in OxCal represents a period of time during which multiple events occurred, but where we don't know (or can't determine) the exact chronological order of those events within the phase, ie there is no stratigraphic relationship between the dated samples. This is particularly relevant for Roman cemetery studies where burials within a cemetery area or burial tradition are assumed to be broadly contemporaneous, even though individual interments may span decades or centuries, and they do not intercut each other.

## Basic Syntax

```
Phase("Phase_Name")
{
    R_Date("Sample_1", radiocarbon_age, error);
    R_Date("Sample_2", radiocarbon_age, error);
    R_Date("Sample_3", radiocarbon_age, error);
};
```

## Key Concepts for Roman Cemetery Dating

### Contemporaneity in Cemetery Context
- All dates within a Phase represent the **same burial tradition or cemetery use period**
- Individual burials may span the entire duration of active cemetery use
- The model estimates when cemetery use began and ended
- No internal chronological ordering of individual burials is imposed

### Statistical Combination
- OxCal uses Bayesian statistics to combine the probability distributions
- Results are typically **more precise** than individual calibrated dates
- Important for distinguishing Roman periods (Early Roman 43-150 AD, Middle Roman 150-250 AD, Late Roman 250-410 AD)
- Outliers (e.g., later Saxon burials, residual Iron Age material) can significantly affect the model

## Simple Phase Model Example

```
Plot()
{
    Phase("Early_Roman_Cemetery_Use")
    {
        R_Date("Burial_12", 1920, 35);    // ~50-130 AD
        R_Date("Burial_45", 1885, 40);   // ~70-220 AD  
        R_Date("Burial_78", 1945, 30);    // ~25-120 AD
        R_Date("Burial_103", 1900, 45);  // ~50-210 AD
    };
};
```

## Archaeological Applications in Roman Cemeteries

### 1. Cemetery Establishment Phase
Dating the initial establishment of a Roman cemetery:

```
Phase("Cemetery_Foundation_Longthorpe")
{
    R_Date("Burial_1", 1950, 35);      // Military cemetery
    R_Date("Burial_3", 1935, 40);  // Early timber coffins
    R_Date("Burial_7e", 1965, 30);    // Conquest period burial
};
```

### 2. Cemetery Use Phases
For burials spanning recognised cemetery periods:

```
Phase("Middle_Roman_Dorchester_Cemetery")
{
    R_Date("Burial_156_Lead_Coffin", 1780, 40);     // ~150-350 AD
    R_Date("Burial_201_Human_Bone", 1820, 35);     // ~130-260 AD
    R_Date("Burial_245_Wood_Coffin", 1795, 45);    // ~140-320 AD
    R_Date("Burial_289_Cremation", 1835, 50);     // ~100-250 AD
};
```

### 3. Late Roman Cemetery Transition
Modeling the transition to Late Roman burial practices:

```
Phase("Late_Roman_Winchester_Burials")
{
    R_Date("Burial_67_Christian_Orientation", 1650, 30);  // ~320-430 AD
    R_Date("Burial_89_Plaster_Burial", 1680, 35);        // ~260-410 AD
    R_Date("Burial_124_Hobnailed_Boots", 1665, 40);      // ~300-420 AD
};
```

## Interpreting Phase Model Results for Roman Cemeteries

### Phase Boundaries
OxCal automatically calculates:
- **Start Boundary**: When cemetery use began
- **End Boundary**: When cemetery use ended (or transitioned)
- **Span**: Duration of active burial activity

### Key Output Parameters for Cemetery Studies
- **Individual Burial Ranges**: Refined calibrated ranges for each burial
- **Cemetery Start/End**: Temporal boundaries of burial activity
- **Cemetery Use Span**: Estimated duration of active use
- **Agreement Indices**: How well burials fit the contemporaneous model

## Worked Example: Colchester Roman Cemetery

```
Plot()
{
    Phase("Balkerne_Lane_Cemetery_Phase_1")
    {
        R_Date("Cremation_Burial_A12", 1940, 30);    // ~40-130 AD
        R_Date("Inhumation_B45", 1925, 35);         // ~50-140 AD  
        R_Date("Cremation_C78", 1955, 25);          // ~30-120 AD
        R_Date("Lead_Coffin_D23", 1910, 40);        // ~60-160 AD
    };
};
```

**Expected Results:**
- Individual burials show **tighter date ranges** than if calibrated separately
- Cemetery start boundary: **50-80 AD** (68% probability) - post-conquest establishment
- Cemetery end boundary: **120-160 AD** (68% probability) - transition to new area
- Cemetery use span: **60-110 years** (68% probability) - typical for Roman urban cemetery


### Problem 1: Very Wide Cemetery Use Span
**Causes:**
- Long-duration cemetery use (common in Roman towns)
- Mixed urban and rural burial traditions
- Cemetery expansion phases
- Curated/heirloom grave goods

**Investigation:**
```
Phase("Long_Use_Canterbury_Cemetery")
{
    R_Date("Early_Military_Burial", 1950, 30);    // ~30-120 AD
    R_Date("Civilian_Expansion", 1850, 35);       // ~90-240 AD
    R_Date("Late_Christian_Burial", 1650, 40);    // ~320-430 AD - 300+ year span
};
```

## Best Practices for Roman Cemetery Studies

### 1. Sample Selection
- Prefer **human bone** over grave goods (avoid heirloom effects)
- Avoid **reused materials** (Roman stones in Saxon contexts)
- Document **burial orientations** (E-W Christian vs. varied pagan)
- Consider **cemetery stratigraphy** and spatial relationships

### 2. Model Validation for Roman Context
- Check **Agreement Indices** (aim for A > 60%)
- Compare with **coin dating** and **pottery sequences**
- Consider **historical context** (conquest 43 AD, Saxon arrival 450+ AD)
- Validate against **established Roman chronologies**

### 3. Interpretation Guidelines
- Cemetery phases represent **burial traditions**, not single events
- Account for **Roman administrative changes** (military to civilian)
- Consider **religious transitions** (pagan to Christian)
- Integrate with **material culture** (brooches, pottery, coins)

## Comparison with Roman Historical Periods

### Phase vs. Historical Chronology
```
// Archaeological Phase Model
Phase("Roman_Winchester_Cemetery")
{
    R_Date("Burial_A", 1850, 30);
    R_Date("Burial_B", 1820, 35);
    R_Date("Burial_C", 1880, 40);
};

// vs. Historical Framework
// Early Roman: 43-150 AD
// Middle Roman: 150-250 AD  
// Late Roman: 250-410 AD
```

### When to Use Phases in Roman Context:
- **Phase**: When burials represent same cemetery tradition
- **Sequence**: When clear cemetery expansion or religious change evident

## Advanced Roman Cemetery Modeling

### Multi-Phase Cemetery Development
```
Sequence("Verulamium_Cemetery_Development")
{
    Boundary("Cemetery_Establishment");
    Phase("Military_Foundation_Burials")
    {
        R_Date("Cremation_Officer", 1955, 35);      // ~30-120 AD
        R_Date("Military_Tombstone", 1940, 30);     // ~40-130 AD
    };
    Boundary("Civilian_Transition");
    Phase("Urban_Cemetery_Expansion")
    {
        R_Date("Merchant_Burial", 1820, 40);        // ~130-260 AD
        R_Date("Craft_Worker_Grave", 1835, 35);     // ~100-250 AD
        R_Date("Child_Burial", 1850, 45);           // ~90-240 AD
    };
    Boundary("Christian_Transition");
    Phase("Late_Roman_Christian_Burials")
    {
        R_Date("E_W_Oriented_Burial", 1670, 30);    // ~260-410 AD
        R_Date("Plaster_Burial", 1650, 35);         // ~320-430 AD
    };
    Boundary("Saxon_Cemetery_Reuse");
};
```

### Regional Cemetery Networks
```
Phase("Hadrian_Wall_Military_Cemeteries")
{
    Phase("Housesteads_Fort_Cemetery")
    {
        R_Date("Auxiliary_Soldier", 1800, 35);      // ~140-330 AD
        R_Date("Military_Dependant", 1820, 40);     // ~130-260 AD
    };
    Phase("Birdoswald_Cemetery")
    {
        R_Date("Cavalry_Burial", 1785, 30);         // ~150-340 AD
        R_Date("Veteran_Settlement", 1750, 45);     // ~210-380 AD
    };
};
```

## Practical Exercise: Roman London Cemetery

**Scenario**: You have four radiocarbon dates from a Roman cemetery in Southwark, London:
- Human bone from cremation burial with Samian pottery: 1890 ± 40 BP
- Wooden coffin fragments from inhumation: 1865 ± 35 BP  
- Human bone from lead coffin burial: 1825 ± 30 BP
- Coffin wood from child burial: 1855 ± 45 BP

**Historical Context**: The cemetery is outside the Roman city walls, typical location for Roman burial practices. Pottery suggests Middle Roman date.

**Task**: Create a Phase model and interpret the results.

```
Plot()
{
    Phase("Southwark_Roman_Cemetery")
    {
        R_Date("Cremation_Samian", 1890, 40);       // ~70-210 AD
        R_Date("Wood_Coffin_Adult", 1865, 35);      // ~80-230 AD
        R_Date("Lead_Coffin_Elite", 1825, 30);      // ~130-260 AD
        R_Date("Child_Burial_Wood", 1855, 45);      // ~90-240 AD
    };
};
```

**Discussion Points**:
1. Do these dates support Middle Roman cemetery use (150-250 AD)?
2. How does the lead coffin date (indicating wealth) fit the sequence?
3. What does the phase span tell us about cemetery duration?
4. How do results compare with London's known Roman chronology?
5. Could any burials represent Late Roman Christian transition?

## Integration with Roman Material Culture

### Combining Radiocarbon with Typological Dating
```
Phase("Roman_Dorchester_Cemetery_Validated")
{
    R_Date("Burial_Trumpet_Brooch", 1920, 35);     // ~50-140 AD (Flavian brooch type)
    R_Date("Burial_Samian_Vessel", 1885, 30);      // ~70-220 AD (Form 37 pottery)
    R_Date("Burial_Coin_Hoard", 1800, 40);        // ~140-330 AD (Antonine coins)
};
```

## Summary for Roman Cemetery Studies

The unordered Phase model is essential for:
- **Combining contemporaneous burials** from Roman cemetery contexts
- **Modeling cemetery use periods** aligned with Roman chronology
- **Distinguishing Roman phases** (Early/Middle/Late Roman periods)
- **Testing assumptions** about cemetery duration and cultural transitions

**Key Considerations for Roman England:**
- Account for **conquest period** establishment (post-43 AD)
- Consider **military to civilian** transitions
- Recognize **pagan to Christian** burial changes
- Integrate with **Roman historical chronology**
- Watch for **Saxon period** intrusions (post-450 AD)

Remember: Roman cemeteries often show continuous use over centuries, making Phase models particularly valuable for understanding burial traditions within broader historical frameworks.

---

*Practice with different Roman cemetery scenarios and always validate your models against established Roman chronologies and material culture sequences.*
