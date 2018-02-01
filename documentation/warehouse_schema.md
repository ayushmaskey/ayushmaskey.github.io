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
|table| proc_ssis | comment |
|-----|-----------|---------|
|dbo.dimDate| built-in sp | one time |
|dbo.cpsSecurity | built-in sp | one time |
|kaiser.kaiserPatientProfile| built-in insert| one time |
|kphcAll.CentricitySecurityDescription| built-in insert | one time |

|cpsAdmin.quickText|    |    |
|cpsAdmin.CentricityGroups|    |    |   
|cpsAdmin.CentricityGroupsUsers|    |    |
|cpsAdmin.CentricitySecurityGiven|    |    |

|dbo.auditData|    |    |
|dbo.employees|    |    |

|dental.slidingFeeCyrca|    |    |

|doh.cvrClient|    |    |
|doh.cvrClientObs|    |    |
|doh.cvrVisitClinicalList|    |    |

|hchp.CBCM_AcuityScore|    |    |
|hchp.cbcm_metric|    |    |
|hchp.CBCMMetricDueNow|    |    |

|kaiser.kaiserVisits|    |    |

|kphc_ad.ADGroup|    |    |
|kphc_ad.ADUSers|    |    |

|kphcAll.Appointment_Activity_Log|    |    |
|kphcAll.Appointments|    |    |
|kphcAll.DocType|    |    |
|kphcAll.Document|    |    |
|kphcAll.Facility|    |    |
|kphcAll.InsuranceCarriers|    |    |
|kphcAll.LogReg|    |    |
|kphcAll.PatientInsurance|    |    |
|kphcAll.PatientProfile|    |    |
|kphcAll.PatientRace|    |    |
|kphcAll.PCPChange|    |    |

|kphcBH.BHMetricDetails|    |    |
|kphcBH.BHMetricDueNow|    |    |
|kphcBH.BHPatients|    |    |

|kphcCC.CCCKD|    |    |
|kphcCC.CCDiabetes|    |    |
|kphcCC.CCHabits|    |    |
|kphcCC.CCHTN|    |    |
|kphcCC.CCSMG|    |    |

|kphcOPT.ContactPrescription|    |    |
|kphcOPT.GlassPrescription|    |    |

|kphcOrders.EnablingCodes|    |    |
|kphcOrders.OrderCategory|    |    |
|kphcOrders.ReferralCodes|    |    |
|kphcOrders.referralFollowup|    |    |
|kphcOrders.Referrals|    |    |
|kphcOrders.referralSetup|    |    |
|kphcOrders.ReferralSpecialist|    |    |

|kphcPP.patientPortalSignup|    |    |

|kphcSara.breast_diagnosis|    |    |
|kphcSara.papHPVTracking|    |    |
|kphcSara.ER_Vsits|    |    |

|Ohana.ProviderNPI|    |    |

|peer.PeerReviewJune2017|    |    |

|uds.CentricityUDS2015|    |    |
|uds.DentricUDS2015|    |    |


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






