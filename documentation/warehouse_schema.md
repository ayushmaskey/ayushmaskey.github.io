create kphcwarehouse
set compatibility level and other settings
add user report with permission db_datareader

need to figure out
kphc-direcotry.dbo.specialist

**create all schema**

| name | use |
|-----|-----|
| kphc_ad |  |
| kphc_all |  |
| kphc_bh |  |
| kphc_cc |  |
| kphc_cps_admin |  |
| kphc_dental |  |
| kphc_doh |  |
| kphc_hchp |  |
| kphc_insurance |  |
| kphc_kaiser |  |
| kphc_kkv |  |
| kphc_opt |  |
| kphc_orders |  |
| kphc_peer |  |
| kphc_pp |  |
| kphc_sara |  |
| kphc_ssis |   |
| kphc_tracking |  |
| kphc_uds |  |
|  |  |
|  |  |

**view **

| name | dependent | use |
|------|-----------|-----|
| kphc_ad.ad_groups_vw |  |  |
| kphc_ad.adComputers_vw |  |  |
| kphc_ad.adusers_vw |  |  |
| kphc_all.controlled_substance_vw |  |  |
| kphc_doh.vwFindCVRPatients |  |  |
| kphc_hchp.vw_CBCM_clients |  |  |
| kphc_insurance.vw_UHC_Medicare_Medicaid_Patient_verified_2017 |  |  |
| kphc_pp.ppAccountsCreated_vw |  |  |
| kphc_sara.abnormalPapMammo_vw |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |


**create table and proc to fill table**

|table| proc_ssis | comment | data test |
|-----|-----------|---------|------|
|kphc_ad.ADGroup|    |    | good |
|kphc_ad.ADUSers|    |    | good |
|kphc_ad.employees|    |    | good |
|-----|-----------|---------|------|
|kphc_all.Appointment_Activity_Log|    |  | nightly | good |
|kphc_all.Appointments|    |  | nightly | good |
|kphc_all.dimDate| built-in sp | one time | good |
|kphc_all.doctorFacility |  |  | nightly | good |
|kphc_all.DocType|    |    | nightly | good |
|kphc_all.Document|    |    | nightly | good |
|kphc_all.Facility|    |    | nightly | good |
|kphc_all.InsuranceCarriers|    |    | nightly | good |
|kphc_all.LogReg|    |    | nightly | good |
|kphc_all.PatientInsurance|    |    | nightly | good |
|kphc_all.PatientProfile|    |    | nightly | good |
|kphc_all.PatientRace|    |    | nightly | good |
|kphc_all.PCPChange|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_bh.BHMetricDetails|    |    |
|kphc_bh.BHMetricDueNow|    |    |
|kphc_bh.BHPatients|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_cc.CCCKD|    |    | nightly | good |
|kphc_cc.CCDiabetes|    |    | nightly | good |
|kphc_cc.CCHabits|    |    | nightly | good |
|kphc_cc.CCHTN|    |    | nightly | good |
|kphc_cc.CCSMG|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_cps_admin.auditData|    |    | nightly | good |
|kphc_cps_admin.CentricityGroups|    |    | nightly | good |
|kphc_cps_admin.CentricityGroupsUsers|    |    | nightly | good |
|kphc_cps_admin.CentricitySecurityDescription| built-in insert | one time |
|kphc_cps_admin.CentricitySecurityGiven|    |    | nightly | good |
|kphc_cps_admin.cpsSecurity | built-in sp | one time | good |
|kphc_cps_admin.quickText|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_dental.slidingFeeCyrca|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_doh.cvrClient|    |    | nightly | good |
|kphc_doh.cvrClientObs|    |    | nightly | good |
|kphc_doh.cvrVisitClinicalList|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_hchp.CBCM_AcuityScore|    |    | nightly | good |
|kphc_hchp.cbcm_metric|    |    | nightly | good |
|kphc_hchp.CBCMMetricDueNow|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_insurance.ER_Vsits|    |    | nightly | good |
|kphc_insurance.ProviderNPI|    |    |
|-----|-----------|---------|------|
|kphc_kaiser.kaiserPatientProfile| built-in insert| one time | good |
|kphc_kaiser.kaiserVisits|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_opt.ContactPrescription|    |    | nightly | good |
|kphc_opt.GlassPrescription|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_orders.EnablingCodes|    |    | nightly | good |
|kphc_orders.OrderCategory|    |    | nightly | good |
|kphc_orders.ReferralCodes|    |    | nightly | good |
|kphc_orders.referralFollowup|    |    | nightly | good |
|kphc_orders.Referrals|    |    | nightly | good |
|kphc_orders.referralSetup|    |    | nightly | good |
|kphc_orders.ReferralSpecialist|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_peer.PeerReviewJune2017|    |    |
|-----|-----------|---------|------|
|kphc_pp.patientPortalSignup|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_sara.breast_diagnosis|    |    | nightly | good |
|kphc_sara.papHPVTracking|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_uds.CentricityUDS2015|    |    |
|kphc_uds.DentricUDS2015|    |    |
|-----|-----------|---------|------|

**SSIS**

| sp name | dependents | use |
|---------|------------|-----|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

**Reports**

| sp name | dependents | use |
|---------|------------|-----|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

**jobs**






