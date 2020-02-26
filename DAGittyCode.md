# Causal Pathways between ADF dispensing and opioid-related mortality

We started by reviewing some [recent background data](https://github.com/opioiddatalab/DAG/blob/master/background.md) on ADF prescribing.<br>

We used [DAGitty (version 3.0)](daggity.net) to identify possible confounders of the relationship between ADF prescribing and overdose death. We simplified the [preivous versions](https://github.com/opioiddatalab/DAG/commits/master/DAGittyCode.md) to consolidate related variables that influenced exposure (e.g., prescribing decisions), but not overdose *per se*. We are considering 42 covariates (listed below), with the main causal pathway of interest being:
<br>

`need for opioids` :arrow_right: `ADF prescribed` :arrow_right: `opioid-related death` 

<br>
Based on the updated DAGitty model, there are 2 possible minimal sufficient adjustment sets for estimating the total effect of ADF on opioid related death:<br>
1. ACE, BMI, Mental Health Disorders, Other substance use disorders, comorbid_conditions_(respiratory_or_metabolic), patient_prior_use_duration, prior_Rx_opioid, take_home_naloxone, unmeasured_confounding<br>
2. BMI, Mental Health Disorders, Other substance use disorders, comorbid_conditions_(respiratory_or_metabolic), patient_prior_use_duration, previous_addiction_tx, prior_Rx_opioid, unmeasured_confounding<br>

![DAG](https://opioiddatalab.github.io/DAG/dagitty-model.png "DAG from Feb 26, 2020")<br>

![DAG Legend](https://opioiddatalab.github.io/DAG/DAGlegend.png "DAGitty legend")<br>

If you want to play with the arrows, here's the code you can copy-paste the code below into [DAGitty](http://www.dagitty.net):<br>

```
dag {
"ADF_use_in_prescriber_professional network" [pos="0.553,1.128"]
"Insurance information" [pos="0.364,-0.172"]
"Mental Health Disorders" [pos="0.497,-0.011"]
"Other substance use disorders" [pos="0.624,0.145"]
"State_and_federal_laws_&_regulations" [pos="0.830,-0.135"]
"comorbid_conditions_(respiratory_or_metabolic)" [pos="0.142,0.278"]
"dose/MME" [pos="0.764,0.647"]
"opioid related death" [outcome,pos="0.846,0.396"]
"prescriber_negative_experience_(ODs_among_patients)" [pos="0.577,0.867"]
ACE [pos="0.841,0.833"]
ADF [exposure,pos="0.516,0.400"]
BMI [pos="0.584,0.309"]
Medicaid_expansion [pos="0.658,-0.078"]
SES [pos="0.216,-0.189"]
cancer_hx [pos="-0.018,0.842"]
clinical_indication [pos="0.201,0.406"]
cost_to_patient [pos="0.265,0.755"]
diverted_Rx_opioid_supply [pos="0.919,0.185"]
expected_patient_opioid_duration [pos="0.138,0.154"]
heroin_supply [pos="0.769,0.195"]
injection [pos="0.675,0.460"]
law_enforcement_interdiction_pressure [pos="0.881,0.037"]
negative_publicity_about_opioids [pos="0.077,-0.061"]
pain_dx [pos="0.098,0.913"]
pain_etiology [pos="0.117,0.777"]
pain_level [pos="0.378,0.540"]
patient_preference [pos="0.232,0.812"]
patient_prior_use_duration [pos="0.031,0.512"]
prescriber_early_adopter [pos="0.483,1.057"]
prescriber_familiarity [pos="0.479,0.945"]
prescriber_mileu [pos="0.563,0.997"]
prescriber_specialty [pos="0.597,0.936"]
prescriber_time_in_practice [pos="0.630,1.059"]
previous_addiction_tx [pos="0.931,0.676"]
prior_Rx_opioid [pos="0.048,0.633"]
race [pos="0.296,0.040"]
smoking [pos="0.318,0.375"]
societal_alarm_about_opioids [pos="0.059,-0.092"]
stability_of_home_environment [pos="0.297,-0.084"]
state_of_residence [pos="0.657,-0.188"]
street_price [pos="0.961,0.329"]
take_home_naloxone [pos="0.961,0.536"]
tampering [pos="0.605,0.583"]
unmeasured_confounding [pos="0.108,1.090"]

"ADF_use_in_prescriber_professional network" -> ADF
"Insurance information" -> ADF
"Mental Health Disorders" -> "opioid related death"
"Mental Health Disorders" -> ADF
"Mental Health Disorders" -> clinical_indication
"Other substance use disorders" -> "opioid related death"
"Other substance use disorders" -> ADF
"Other substance use disorders" -> tampering
"State_and_federal_laws_&_regulations" -> "Insurance information"
"State_and_federal_laws_&_regulations" -> Medicaid_expansion
"comorbid_conditions_(respiratory_or_metabolic)" -> "opioid related death"
"comorbid_conditions_(respiratory_or_metabolic)" -> ADF
"comorbid_conditions_(respiratory_or_metabolic)" -> clinical_indication
"dose/MME" -> "opioid related death"
"prescriber_negative_experience_(ODs_among_patients)" -> ADF
ACE -> "opioid related death"
ACE -> previous_addiction_tx
ADF -> "dose/MME"
ADF -> "opioid related death"
ADF -> injection
ADF -> tampering
BMI -> "opioid related death"
BMI -> ADF
Medicaid_expansion -> "Insurance information"
SES -> "Insurance information"
SES -> stability_of_home_environment
cancer_hx -> pain_etiology
clinical_indication -> ADF
clinical_indication -> pain_level
clinical_indication -> smoking
cost_to_patient -> ADF
diverted_Rx_opioid_supply -> street_price
expected_patient_opioid_duration -> clinical_indication
heroin_supply -> "opioid related death"
heroin_supply -> diverted_Rx_opioid_supply
injection -> "opioid related death"
law_enforcement_interdiction_pressure -> diverted_Rx_opioid_supply
law_enforcement_interdiction_pressure -> heroin_supply
law_enforcement_interdiction_pressure -> street_price
negative_publicity_about_opioids -> ADF
pain_dx -> pain_etiology
pain_etiology -> clinical_indication
pain_level -> ADF
patient_preference -> ADF
patient_prior_use_duration -> "dose/MME"
patient_prior_use_duration -> ADF
patient_prior_use_duration -> clinical_indication
prescriber_early_adopter -> ADF
prescriber_early_adopter -> prescriber_familiarity
prescriber_familiarity -> ADF
prescriber_mileu -> ADF
prescriber_specialty -> ADF
prescriber_time_in_practice -> ADF
previous_addiction_tx -> ADF
previous_addiction_tx -> take_home_naloxone
prior_Rx_opioid -> "dose/MME"
prior_Rx_opioid -> ADF
prior_Rx_opioid -> clinical_indication
race -> ADF
smoking -> ADF
societal_alarm_about_opioids -> ADF
stability_of_home_environment -> ADF
street_price -> "opioid related death"
take_home_naloxone -> "opioid related death"
tampering -> injection
unmeasured_confounding -> "opioid related death"
unmeasured_confounding -> ADF
}

```

Credit for DAGitty goes to:
Johannes Textor, Benito van der Zander, Mark K. Gilthorpe, Maciej Liskiewicz, George T.H. Ellison.
[Robust causal inference using directed acyclic graphs: the R package 'dagitty'.](http://johannes-textor.name/papers/2017-ije.pdf)
<i>International Journal of Epidemiology</i>, 45(6):1887-1894, 2016.

---

# Discussion Debrief
The discussion was held via telecon on 26-February 2020, with FDA, UNC and UK attendees.<br>

**Suggestions**
+ Prior (non-fatal) OD history is documented in claims data, so these should be included as a potential time-varying confounder, along with other comorbidities.
+ Concurrent benzodiazepine prescribing should be added to the list of potential confounders
+ Aggregating prescriber characteristics (bottom green cluster) makes sense, especially since they only go into ADF prescribing decision box. However, the implications of the [ICPE abstract](https://opioiddatalab.github.io/PharmacistPrescriberSurveys/earlyAdopters/ICPEabstractEarlyPrescribers_submitted.html) finding (early prescribers may be more likely to use risk stratification tools) suggests a potential confounder path between ADF prescribing and overdose outcome. This should be added to the model above for assessment. This could be operationalized by looking at the prescribing of other newly marketed drugs in claims data (including non-opioids).
+ Is there time-varying selection bias if there have been fundamental shift over the past decade in what kind of pain requires opioids? What are the implications of including `need for opioids` on the causal pathway? Does *not* including it (e.g., focusing only on `ADF prescribed` :arrow_right: `opioid-related death`) induce selection bias over time, in that people who would have gotten opioids earlier would not later for the same condition? To what extent can baseline adjustment help with this?<br>
`need for opioids` :arrow_right: `ADF prescribed` :arrow_right: `opioid-related death` <br>
+ Are there other time-varying secular trends (e.g., Medicaid expansion) that should be accounted for? In one way we are selecting people with insurance in the KY Medicaid and NC BCBS populations; and we can continue to follow using PDMP data in KY even after loss of eligibility. 



