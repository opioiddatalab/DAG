# DAGitty code to reproduce our base DAG

We used [DAGitty (version 2.3)] to identify possible confounders of the relationship between ADF prescribing and overdose death.

Based on the arrows we drew so far, there are 5 possible minimal sufficient adjustment sets for estimating the total effect of ADF on opioid related death:
1. ACE, BMI, clinical_indication, prior_Rx_opioid, take_home_naloxone, unmeasured_confounding
2. ACE, BMI, comorbid_conditions_(respiratory_or_metabolic), take_home_naloxone, unmeasured_confounding or
3. BMI, clinical_indication, previous_addiction_tx, prior_Rx_opioid, unmeasured_confounding or
4. BMI, comorbid_conditions_(respiratory_or_metabolic), previous_addiction_tx, unmeasured_confounding or
5. prescriber_familiarity, prescriber_specialty, prescribing_decision, unmeasured_confounding

If you want to play with the arrows, here's the code you can copy-paste the code below into [DAGitty](http://www.dagitty.net) to recreate [our DAG](https://github.com/opioiddatalab/DAG/blob/master/dagitty-model.pdf):

```ACA 1 @0.466,-0.170
ACE 1 @0.928,0.863
ADF E @0.516,0.400
ADF_use_in_prescriber_professional%20network 1 @0.843,0.939
BMI 1 @0.584,0.309
Medicaid_expansion 1 @0.674,-0.024
SES 1 @-0.016,-0.166
State_and_federal_laws_%26_regulations 1 @0.886,-0.098
cancer_hx 1 @-0.018,0.842
clinical_indication 1 @0.201,0.406
comorbid_conditions_(respiratory_or_metabolic) 1 @0.142,0.278
cost_to_patient 1 @0.339,0.789
diverted_Rx_opioid_supply 1 @0.919,0.185
dose%2FMME 1 @0.764,0.647
expected_patient_opioid_duration 1 @0.138,0.154
heroin_supply 1 @0.724,0.253
injection 1 @0.675,0.460
insurance_rules_(prior_auth%2C_parity) 1 @0.374,-0.085
insurance_type 1 @0.255,-0.166
insurance_y%2Fn 1 @0.119,-0.163
law_enforcement_interdiction_pressure 1 @0.881,0.037
level_of_alcohol_use 1 @0.420,0.050
negative_publicity_about_opioids 1 @0.293,1.025
opioid%20related%20death O @0.846,0.396
pain_dx 1 @0.098,0.913
pain_etiology 1 @0.117,0.777
pain_level 1 @0.016,0.982
patient_preference 1 @0.230,0.737
patient_prior_use_duration 1 @0.049,0.437
prescriber_early_adopter 1 @0.476,1.097
prescriber_familiarity 1 @0.431,0.937
prescriber_mileu 1 @0.598,1.025
prescriber_negative_experience_(ODs_among_patients) 1 @0.199,0.611
prescriber_specialty 1 @0.778,1.101
prescriber_time_in_practice 1 @0.667,0.098
prescribing_decision 1 @0.350,0.400
previous_addiction_tx 1 @0.931,0.676
prior_Rx_opioid 1 @0.056,0.559
race 1 @0.238,0.089
smoking 1 @0.313,0.190
societal_alarm_about_opioids 1 @0.105,0.014
stability_of_home_environment 1 @0.520,0.174
state_of_residence 1 @0.657,-0.188
street_price 1 @0.961,0.329
take_home_naloxone 1 @0.961,0.536
tampering 1 @0.553,0.590
unmeasured_confounding 1 @0.108,1.090

ACA Medicaid_expansion insurance_rules_(prior_auth%2C_parity)
ACE opioid%20related%20death previous_addiction_tx
ADF dose%2FMME injection opioid%20related%20death tampering
ADF_use_in_prescriber_professional%20network ADF
BMI opioid%20related%20death prescribing_decision
Medicaid_expansion insurance_rules_(prior_auth%2C_parity)
SES insurance_y%2Fn
State_and_federal_laws_%26_regulations ACA state_of_residence
cancer_hx pain_etiology
clinical_indication prescribing_decision
comorbid_conditions_(respiratory_or_metabolic) clinical_indication opioid%20related%20death
cost_to_patient ADF
diverted_Rx_opioid_supply street_price
dose%2FMME opioid%20related%20death
expected_patient_opioid_duration clinical_indication
heroin_supply diverted_Rx_opioid_supply opioid%20related%20death
injection opioid%20related%20death
insurance_rules_(prior_auth%2C_parity) prescribing_decision
insurance_type insurance_rules_(prior_auth%2C_parity)
insurance_y%2Fn insurance_type
law_enforcement_interdiction_pressure diverted_Rx_opioid_supply heroin_supply street_price
level_of_alcohol_use prescribing_decision
negative_publicity_about_opioids prescribing_decision
pain_dx pain_etiology
pain_etiology clinical_indication
pain_level clinical_indication
patient_preference prescribing_decision
patient_prior_use_duration clinical_indication
prescriber_early_adopter ADF prescriber_familiarity
prescriber_familiarity ADF prescribing_decision
prescriber_mileu prescribing_decision
prescriber_negative_experience_(ODs_among_patients) prescribing_decision
prescriber_specialty ADF prescribing_decision
prescriber_time_in_practice prescribing_decision
prescribing_decision ADF
previous_addiction_tx prescribing_decision take_home_naloxone
prior_Rx_opioid clinical_indication prescribing_decision
race prescribing_decision
smoking prescribing_decision
societal_alarm_about_opioids prescribing_decision
stability_of_home_environment prescribing_decision
state_of_residence ACA Medicaid_expansion
street_price opioid%20related%20death
take_home_naloxone opioid%20related%20death
tampering injection
unmeasured_confounding ADF opioid%20related%20death
```

Credit for DAGitty goes to:
Johannes Textor, Benito van der Zander, Mark K. Gilthorpe, Maciej Liskiewicz, George T.H. Ellison.
[Robust causal inference using directed acyclic graphs: the R package 'dagitty'.](http://johannes-textor.name/papers/2017-ije.pdf)
<i>International Journal of Epidemiology</i>, 45(6):1887-1894, 2016.
