# Denwire Sales Order Tables (SO)

Tables prefixed `so` belong to the Sales Order module of the Strategix ERP system.
Column prefixes are abbreviated forms of the table name (e.g. `soh_` = sohead).

---

## sohead — Order Header

The main sales order header record. One row per order.

| Column | Type | Nulls |
|--------|------|-------|
| soh_account | char(10) | yes |
| soh_ordref | char(8) | yes |
| soh_ordver | smallint | yes |
| soh_userid | char(4) | yes |
| soh_deladd | char(4) | yes |
| soh_cusref | char(25) | yes |
| soh_repcode | char(4) | yes |
| soh_area | char(4) | yes |
| soh_plist | char(1) | yes |
| soh_cdisc | char(1) | yes |
| soh_orddate | date | yes |
| soh_ordtype | char(1) | yes |
| soh_reqdate | date | yes |
| soh_status | char(1) | yes |
| soh_stloc | char(5) | yes |
| soh_altloc | char(5) | yes |
| soh_neword | char(1) | yes |
| soh_delname | char(40) | yes |
| soh_delad1 | char(30) | yes |
| soh_delad2 | char(30) | yes |
| soh_delad3 | char(30) | yes |
| soh_delad4 | char(30) | yes |
| soh_delad5 | char(30) | yes |
| soh_delpost | char(10) | yes |
| soh_nextsuf | smallint | yes |
| soh_acknow | char(1) | yes |
| soh_despfl | char(1) | yes |
| soh_partdel | char(1) | yes |
| soh_deltyp | char(1) | yes |
| soh_comdel | char(1) | yes |
| soh_invflag | char(1) | yes |
| soh_partinv | char(1) | yes |
| soh_ndcode | char(10) | yes |
| soh_ordval | float | yes |
| soh_outvat | float | yes |
| soh_ordwght | float | yes |
| soh_ordcost | float | yes |
| soh_invval | float | yes |
| soh_export | char(1) | yes |
| soh_trcode | char(1) | yes |
| soh_transp | char(30) | yes |
| soh_vanarea | char(4) | yes |
| soh_class | char(4) | yes |
| soh_sepinvord | char(1) | yes |
| soh_spinvdel | char(1) | yes |
| soh_currency | char(4) | yes |
| soh_terms | char(4) | yes |
| soh_lbulkref | integer | yes |
| soh_repnum | smallint | yes |
| soh_reptim | char(1) | yes |
| soh_repint | smallint | yes |
| soh_repday | smallint | yes |
| soh_stopcode | char(1) | yes |
| soh_fwdflag | char(1) | yes |
| soh_payval | float | yes |
| soh_invform | char(8) | yes |
| soh_ordpri | char(1) | yes |
| soh_txregno | char(15) | yes |
| soh_cvrate | float | yes |
| soh_stockdate | date | yes |
| soh_numacknow | smallint | yes |
| soh_div | char(4) | yes |
| soh_origval | float | yes |
| soh_ediinv | char(1) | yes |
| soh_deltel | char(20) | yes |
| soh_valdate | date | yes |
| soh_xchgrate | float | yes |
| soh_xchgvar | float | yes |
| soh_taxstat | char(1) | yes |
| soh_loadno | integer | yes |
| soh_extstat | char(1) | yes |
| soh_usesched | char(1) | yes |
| soh_wt | char(2) | yes |
| soh_job | char(10) | yes |
| soh_subcode | char(4) | yes |
| soh_security | char(1) | yes |
| soh_delfax | char(20) | yes |
| soh_delcon | char(30) | yes |
| soh_tpacks | float | yes |
| soh_repgen | char(1) | yes |
| soh_author | char(4) | yes |
| soh_master | char(1) | yes |
| soh_mastord | char(8) | yes |
| soh_source | char(8) | yes |
| soh_custconf | char(1) | yes |
| soh_cocreq | char(1) | yes |
| soh_ref1 | char(15) | yes |
| soh_ref2 | char(15) | yes |
| soh_pdate | char(1) | yes |
| soh_delterm | char(3) | yes |
| soh_origref | char(8) | yes |
| soh_qtestatus | char(1) | yes |
| soh_qtedate | date | yes |
| soh_reason | char(1) | yes |
| soh_odisct | char(1) | yes |
| soh_odscc | char(10) | yes |
| soh_credval | float | yes |
| soh_credvt | float | yes |
| soh_company | char(4) | yes |
| soh_cusndcode | char(10) | yes |
| soh_cragtyp | char(6) | yes |
| soh_crprov | char(2) | yes |
| soh_authref | char(12) | yes |
| soh_antcode | integer | yes |
| soh_invvat | float | yes |
| soh_hlddate | date | yes |
| soh_alldays | smallint | yes |
| soh_paymeth | char(1) | yes |
| soh_masttype | char(1) | yes |
| soh_autoproc | char(1) | yes |
| soh_code1 | char(5) | yes |
| soh_code2 | char(5) | yes |
| soh_code3 | char(5) | yes |
| soh_credcont | char(4) | yes |
| soh_maxdel | smallint | yes |
| soh_deltot | smallint | yes |
| soh_pickpri | smallint | yes |
| soh_nopick | char(1) | yes |
| soh_deldays | char(7) | yes |
| soh_pigrp | char(3) | yes |
| soh_ackmeth | char(1) | yes |
| soh_serlev | char(4) | yes |
| soh_leaseacc | char(10) | yes |
| soh_leaseord | char(1) | yes |
| soh_leaseref | char(25) | yes |

---

## soitem — Order Line Items

One row per line on a sales order. Links to sohead via soi_ordref.

| Column | Type | Nulls |
|--------|------|-------|
| soi_ordref | char(8) | yes |
| soi_seq | smallint | yes |
| soi_linseq | smallint | yes |
| soi_ittype | char(1) | yes |
| soi_itstk | char(1) | yes |
| soi_product | char(40) | yes |
| soi_desc | char(40) | yes |
| soi_itqty | float | yes |
| soi_price | float | yes |
| soi_per | float | yes |
| soi_uom | char(1) | yes |
| soi_convert | float | yes |
| soi_itstat | char(1) | yes |
| soi_ndeldat | date | yes |
| soi_weight | float | yes |
| soi_vol | float | yes |
| soi_invval | float | yes |
| soi_itcost | float | yes |
| soi_cossal | float | yes |
| soi_bulkref | integer | yes |
| soi_discper | float | yes |
| soi_suffix | smallint | yes |
| soi_lineref | smallint | yes |
| soi_pdisc | float | yes |
| soi_gdisc | float | yes |
| soi_odisc | float | yes |
| soi_stloc | char(5) | yes |
| soi_psource | char(1) | yes |
| soi_vatcode | char(1) | yes |
| soi_invref | char(8) | yes |
| soi_secref | char(8) | yes |
| soi_delref | char(8) | yes |
| soi_poline | integer | yes |
| soi_batch | integer | yes |
| soi_bin | char(10) | yes |
| soi_custprod | char(40) | yes |
| soi_claim | integer | yes |
| soi_quotref | char(8) | yes |
| soi_stockdate | date | yes |
| soi_reqdate | date | yes |
| soi_comdt1 | date | yes |
| soi_comdt2 | date | yes |
| soi_valudisc | float | yes |
| soi_adjqty | float | yes |
| soi_entqty | float | yes |
| soi_basepri | float | yes |
| soi_spdisc | float | yes |
| soi_stopcode | char(1) | yes |
| soi_clmval | float | yes |
| soi_invdate | date | yes |
| soi_loadno | integer | yes |
| soi_extstat | char(1) | yes |
| soi_usesched | char(1) | yes |
| soi_tcode | integer | yes |
| soi_cprice | char(1) | yes |
| soi_time | float | yes |
| soi_atype | char(1) | yes |
| soi_wotype | char(1) | yes |
| soi_parent | smallint | yes |
| soi_despdate | date | yes |
| soi_desaudit | integer | yes |
| soi_mastline | smallint | yes |
| soi_reack | char(1) | yes |
| soi_cusloc | char(10) | yes |
| soi_cusitem | char(6) | yes |
| soi_itweight | float | yes |
| soi_nettpri | char(1) | yes |
| soi_gdisct | char(1) | yes |
| soi_gdscc | char(10) | yes |
| soi_upcossal | float | yes |
| soi_rep | char(4) | yes |
| soi_billdate | date | yes |
| soi_pickqty | float | yes |
| soi_smwt | char(2) | yes |
| soi_smjob | char(10) | yes |
| soi_smline | integer | yes |
| soi_linkcurr | char(5) | yes |
| soi_cstbasis | float | yes |
| soi_linkrate | float | yes |
| soi_uplinkvar | float | yes |
| soi_lolinkvar | float | yes |
| soi_curradj | float | yes |
| soi_unres | char(1) | yes |
| soi_vanarea | char(4) | yes |
| soi_rmaref | char(8) | yes |
| soi_supplier | char(10) | yes |
| soi_branch | char(4) | yes |
| soi_potype | char(1) | yes |
| soi_costex | char(1) | yes |
| soi_xcode1 | char(5) | yes |
| soi_xcode2 | char(5) | yes |
| soi_xcode3 | char(5) | yes |
| soi_canqty | float | yes |
| soi_pigrp | char(3) | yes |
| soi_waction | smallint | yes |

---

## soinvoice — Invoice Header

Invoice records generated from sales orders.

| Column | Type | Nulls |
|--------|------|-------|
| soinv_invref | char(8) | yes |
| soinv_ordref | char(8) | yes |
| soinv_account | char(10) | yes |
| soinv_edino | char(10) | yes |
| soinv_invdate | date | yes |
| soinv_doctot | float | yes |
| soinv_vatc1 | char(1) | yes |
| soinv_vatc2 | char(1) | yes |
| soinv_vatc3 | char(1) | yes |
| soinv_vatc4 | char(1) | yes |
| soinv_vatc5 | char(1) | yes |
| soinv_gds1 | float | yes |
| soinv_gds2 | float | yes |
| soinv_gds3 | float | yes |
| soinv_gds4 | float | yes |
| soinv_gds5 | float | yes |
| soinv_gdstot | float | yes |
| soinv_setdisc | float | yes |
| soinv_setlpc | float | yes |
| soinv_termdesc | char(30) | yes |
| soinv_totdisc | float | yes |
| soinv_vrate1 | float | yes |
| soinv_vrate2 | float | yes |
| soinv_vrate3 | float | yes |
| soinv_vrate4 | float | yes |
| soinv_vrate5 | float | yes |
| soinv_vatexch | float | yes |
| soinv_proof | integer | yes |
| soinv_type | char(1) | yes |
| soinv_glbatch | char(6) | yes |
| soinv_currency | char(4) | yes |
| soinv_vat1 | float | yes |
| soinv_vat2 | float | yes |
| soinv_vat3 | float | yes |
| soinv_vat4 | float | yes |
| soinv_vat5 | float | yes |

---

## sodeliv — Delivery Header

Delivery records linked to orders. One per delivery consignment.

| Column | Type | Nulls |
|--------|------|-------|
| sod_pikloc | char(5) | yes |
| sod_account | char(10) | yes |
| sod_deladd | char(4) | yes |
| sod_ordref | char(8) | yes |
| sod_suffix | smallint | yes |
| sod_bulkref | integer | yes |
| sod_pickdat | date | yes |
| sod_delstat | smallint | yes |
| sod_delcomb | smallint | yes |
| sod_parcels | smallint | yes |
| sod_delref | char(8) | yes |
| sod_receiver | char(30) | yes |
| sod_delname | char(40) | yes |
| sod_delad1 | char(30) | yes |
| sod_delad2 | char(30) | yes |
| sod_delad3 | char(30) | yes |
| sod_delad4 | char(30) | yes |
| sod_delad5 | char(30) | yes |
| sod_delpost | char(10) | yes |
| sod_carrier | char(10) | yes |
| sod_carser | char(10) | yes |
| sod_custref | char(20) | yes |
| sod_condate | date | yes |
| sod_contime | smallfloat | yes |
| sod_deldate | date | yes |
| sod_deltime | smallfloat | yes |
| sod_nobox | smallint | yes |
| sod_ccharge | float | yes |
| sod_picker | char(10) | yes |
| sod_packer | char(10) | yes |
| sod_confirmed | char(1) | yes |
| sod_company | char(4) | yes |
| sod_pickprnt | smallint | yes |
| sod_loadno | integer | yes |
| sod_colldate | date | yes |
| sod_colltime | smallfloat | yes |
| sod_totwght | float | yes |

---

## sohish — Order History Header

Historical snapshot of sohead records (same structure as sohead, prefix sos_).

| Column | Type | Nulls |
|--------|------|-------|
| sos_account | char(10) | yes |
| sos_ordref | char(8) | yes |
| sos_ordver | smallint | yes |
| sos_userid | char(4) | yes |
| sos_deladd | char(4) | yes |
| sos_cusref | char(25) | yes |
| sos_repcode | char(4) | yes |
| sos_area | char(4) | yes |
| sos_plist | char(1) | yes |
| sos_cdisc | char(1) | yes |
| sos_orddate | date | yes |
| sos_ordtype | char(1) | yes |
| sos_reqdate | date | yes |
| sos_status | char(1) | yes |
| sos_stloc | char(5) | yes |
| sos_altloc | char(5) | yes |
| sos_neword | char(1) | yes |
| sos_delname | char(40) | yes |
| sos_delad1 | char(30) | yes |
| sos_delad2 | char(30) | yes |
| sos_delad3 | char(30) | yes |
| sos_delad4 | char(30) | yes |
| sos_delad5 | char(30) | yes |
| sos_delpost | char(10) | yes |
| sos_nextsuf | smallint | yes |
| sos_acknow | char(1) | yes |
| sos_despfl | char(1) | yes |
| sos_partdel | char(1) | yes |
| sos_deltyp | char(1) | yes |
| sos_comdel | char(1) | yes |
| sos_invflag | char(1) | yes |
| sos_partinv | char(1) | yes |
| sos_ndcode | char(10) | yes |
| sos_ordval | float | yes |
| sos_outvat | float | yes |
| sos_ordwght | float | yes |
| sos_ordcost | float | yes |
| sos_invval | float | yes |
| sos_export | char(1) | yes |
| sos_trcode | char(1) | yes |
| sos_transp | char(30) | yes |
| sos_vanarea | char(4) | yes |
| sos_class | char(4) | yes |
| sos_sepinvord | char(1) | yes |
| sos_spinvdel | char(1) | yes |
| sos_currency | char(4) | yes |
| sos_terms | char(4) | yes |
| sos_lbulkref | integer | yes |
| sos_repnum | smallint | yes |
| sos_reptim | char(1) | yes |
| sos_repint | smallint | yes |
| sos_repday | smallint | yes |
| sos_stopcode | char(1) | yes |
| sos_fwdflag | char(1) | yes |
| sos_payval | float | yes |
| sos_invform | char(8) | yes |
| sos_ordpri | char(1) | yes |
| sos_txregno | char(15) | yes |
| sos_cvrate | float | yes |
| sos_stockdate | date | yes |
| sos_numacknow | smallint | yes |
| sos_div | char(4) | yes |
| sos_origval | float | yes |
| sos_ediinv | char(1) | yes |
| sos_deltel | char(20) | yes |
| sos_valdate | date | yes |
| sos_xchgrate | float | yes |
| sos_xchgvar | float | yes |
| sos_taxstat | char(1) | yes |
| sos_loadno | integer | yes |
| sos_extstat | char(1) | yes |
| sos_usesched | char(1) | yes |
| sos_wt | char(2) | yes |
| sos_job | char(10) | yes |
| sos_subcode | char(4) | yes |
| sos_delfax | char(20) | yes |
| sos_delcon | char(30) | yes |
| sos_tpacks | float | yes |
| sos_author | char(4) | yes |
| sos_master | char(1) | yes |
| sos_mastord | char(8) | yes |
| sos_source | char(8) | yes |
| sos_custconf | char(1) | yes |
| sos_cocreq | char(1) | yes |
| sos_ref1 | char(15) | yes |
| sos_ref2 | char(15) | yes |
| sos_pdate | char(1) | yes |
| sos_delterm | char(3) | yes |
| sos_origref | char(8) | yes |
| sos_qtestatus | char(1) | yes |
| sos_qtedate | date | yes |
| sos_reason | char(1) | yes |
| sos_odisct | char(1) | yes |
| sos_odscc | char(10) | yes |
| sos_company | char(4) | yes |
| sos_cusndcode | char(10) | yes |
| sos_cragtyp | char(6) | yes |
| sos_crprov | char(2) | yes |
| sos_authref | char(12) | yes |
| sos_antcode | integer | yes |
| sos_invvat | float | yes |
| sos_paymeth | char(1) | yes |
| sos_masttype | char(1) | yes |
| sos_autoproc | char(1) | yes |
| sos_code1 | char(5) | yes |
| sos_code2 | char(5) | yes |
| sos_code3 | char(5) | yes |
| sos_credcont | char(1) | yes |
| sos_maxdel | smallint | yes |
| sos_deltot | smallint | yes |
| sos_pickpri | smallint | yes |
| sos_pigrp | char(3) | yes |
| sos_ackmeth | char(1) | yes |
| sos_serlev | char(4) | yes |
| sos_leaseacc | char(10) | yes |
| sos_leaseord | char(1) | yes |

---

## soitemh — Order Items History

Historical snapshot of soitem records (same structure as soitem, prefix soz_).

| Column | Type | Nulls |
|--------|------|-------|
| soz_ordref | char(8) | yes |
| soz_seq | smallint | yes |
| soz_linseq | smallint | yes |
| soz_ittype | char(1) | yes |
| soz_itstk | char(1) | yes |
| soz_product | char(40) | yes |
| soz_desc | char(40) | yes |
| soz_itqty | float | yes |
| soz_price | float | yes |
| soz_per | float | yes |
| soz_uom | char(1) | yes |
| soz_convert | float | yes |
| soz_itstat | char(1) | yes |
| soz_ndeldat | date | yes |
| soz_weight | float | yes |
| soz_vol | float | yes |
| soz_invval | float | yes |
| soz_itcost | float | yes |
| soz_cossal | float | yes |
| soz_bulkref | integer | yes |
| soz_discper | float | yes |
| soz_suffix | smallint | yes |
| soz_lineref | smallint | yes |
| soz_pdisc | float | yes |
| soz_gdisc | float | yes |
| soz_odisc | float | yes |
| soz_stloc | char(5) | yes |
| soz_psource | char(1) | yes |
| soz_vatcode | char(1) | yes |
| soz_invref | char(8) | yes |
| soz_secref | char(8) | yes |
| soz_delref | char(8) | yes |
| soz_poline | integer | yes |
| soz_batch | integer | yes |
| soz_bin | char(10) | yes |
| soz_custprod | char(40) | yes |
| soz_claim | integer | yes |
| soz_quotref | char(8) | yes |
| soz_stockdate | date | yes |
| soz_reqdate | date | yes |
| soz_comdt1 | date | yes |
| soz_comdt2 | date | yes |
| soz_valudisc | float | yes |
| soz_adjqty | float | yes |
| soz_entqty | float | yes |
| soz_basepri | float | yes |
| soz_spdisc | float | yes |
| soz_stopcode | char(1) | yes |
| soz_clmval | float | yes |
| soz_invdate | date | yes |
| soz_loadno | integer | yes |
| soz_extstat | char(1) | yes |
| soz_usesched | char(1) | yes |
| soz_tcode | integer | yes |
| soz_cprice | char(1) | yes |
| soz_time | float | yes |
| soz_atype | char(1) | yes |
| soz_parent | smallint | yes |
| soz_mastline | smallint | yes |
| soz_reack | char(1) | yes |
| soz_cusloc | char(10) | yes |
| soz_cusitem | char(6) | yes |
| soz_itweight | float | yes |
| soz_nettpri | char(1) | yes |
| soz_gdisct | char(1) | yes |
| soz_gdscc | char(10) | yes |
| soz_upcossal | float | yes |
| soz_rep | char(4) | yes |
| soz_billdate | date | yes |
| soz_smwt | char(2) | yes |
| soz_smjob | char(10) | yes |
| soz_smline | integer | yes |
| soz_linkcurr | char(5) | yes |
| soz_cstbasis | float | yes |
| soz_linkrate | float | yes |
| soz_uplinkvar | float | yes |
| soz_lolinkvar | float | yes |
| soz_curradj | float | yes |
| soz_vanarea | char(4) | yes |
| soz_rmaref | char(8) | yes |
| soz_supplier | char(10) | yes |
| soz_branch | char(4) | yes |
| soz_potype | char(1) | yes |
| soz_costex | char(1) | yes |
| soz_xcode1 | char(5) | yes |
| soz_xcode2 | char(5) | yes |
| soz_xcode3 | char(5) | yes |
| soz_pigrp | char(3) | yes |

---

## sorhead — Returns Header

Header for customer returns (RMA).

| Column | Type | Nulls |
|--------|------|-------|
| sorh_retno | char(8) | yes |
| sorh_customer | char(10) | yes |
| sorh_sloc | char(5) | yes |
| sorh_origso | char(8) | yes |
| sorh_dateret | date | yes |
| sorh_datecom | date | yes |
| sorh_status | char(1) | yes |
| sorh_soref | char(8) | yes |
| sorh_crref | char(8) | yes |
| sorh_poref | char(13) | yes |
| sorh_reason | char(4) | yes |
| sorh_version | integer | yes |
| sorh_notereq | char(1) | yes |
| sorh_cusdoc | char(15) | yes |
| sorh_auth | char(4) | yes |
| sorh_repcode | char(4) | yes |
| sorh_area | char(4) | yes |
| sorh_delcode | char(4) | yes |
| sorh_caddr | char(10) | yes |
| sorh_colname | char(40) | yes |
| sorh_colad1 | char(30) | yes |
| sorh_colad2 | char(30) | yes |
| sorh_colad3 | char(30) | yes |
| sorh_colad4 | char(30) | yes |
| sorh_colad5 | char(30) | yes |
| sorh_colpost | char(10) | yes |
| sorh_coltel | char(20) | yes |
| sorh_colfax | char(20) | yes |
| sorh_cnote | char(10) | yes |
| sorh_loadno | integer | yes |
| sorh_contact | char(30) | yes |
| sorh_transp | char(30) | yes |
| sorh_vanarea | char(4) | yes |
| sorh_inext | char(1) | yes |
| sorh_extstat | char(1) | yes |
| sorh_company | char(4) | yes |
| sorh_cusndcode | char(10) | yes |

---

## soritem — Returns Line Items

Line items on a customer return. Links to sorhead via sori_retno.

| Column | Type | Nulls |
|--------|------|-------|
| sori_retno | char(8) | yes |
| sori_seq | integer | yes |
| sori_product | char(40) | yes |
| sori_qty | float | yes |
| sori_uom | char(1) | yes |
| sori_loc | char(5) | yes |
| sori_bin | char(10) | yes |
| sori_costpr | float | yes |
| sori_sellpr | float | yes |
| sori_act1 | char(4) | yes |
| sori_opid1 | char(4) | yes |
| sori_date1 | date | yes |
| sori_stat1 | char(1) | yes |
| sori_act2 | char(4) | yes |
| sori_opid2 | char(4) | yes |
| sori_date2 | date | yes |
| sori_stat2 | char(1) | yes |
| sori_origso | char(8) | yes |
| sori_poref | char(13) | yes |
| sori_defect | char(4) | yes |
| sori_reason | char(4) | yes |
| sori_nolabs | integer | yes |

---

## sopick — Pick List Header

Pick list header records for warehouse picking.

| Column | Type | Nulls |
|--------|------|-------|
| sopi_pid | integer | yes |
| sopi_ordref | char(8) | yes |
| sopi_status | char(1) | yes |
| sopi_loc | char(5) | yes |
| sopi_pickdate | date | yes |
| sopi_picktime | smallfloat | yes |
| sopi_lineno | smallint | yes |
| sopi_suffix | smallint | yes |
| sopi_bulkref | integer | yes |

---

## sounpick — Unpick Records

Records of items that have been un-picked (reversed picks).

| Column | Type | Nulls |
|--------|------|-------|
| soun_ordref | char(8) | yes |
| soun_line | smallint | yes |
| soun_unqkey | serial | no |
| soun_batch | integer | yes |
| soun_bin | char(10) | yes |
| soun_serial | char(22) | yes |
| soun_qty | float | yes |
| soun_trandate | date | yes |

---

## socomm — Order Line Comments

Free text comment lines attached to order lines.

| Column | Type | Nulls |
|--------|------|-------|
| socom_ordref | char(8) | yes |
| socom_ordline | smallint | yes |
| socom_comseq | smallint | yes |
| socom_comtype | char(1) | yes |
| socom_text | char(50) | yes |

---

## sorcomm — Returns Comments

Free text comment lines on return records.

| Column | Type | Nulls |
|--------|------|-------|
| sorc_retno | char(8) | yes |
| sorc_line | integer | yes |
| sorc_seq | integer | yes |
| sorc_text | char(50) | yes |

---

## soaudit — Order Audit Trail

Audit trail of changes made to sales orders.

| Column | Type | Nulls |
|--------|------|-------|
| sou_user | char(4) | yes |
| sou_ordref | char(8) | yes |
| sou_type | char(1) | yes |
| sou_product | char(40) | yes |
| sou_desc | char(40) | yes |
| sou_before | float | yes |
| sou_after | float | yes |
| sou_datover | date | yes |
| sou_seq | integer | yes |
| sou_proof | smallint | yes |
| sou_account | char(10) | yes |
| sou_timeover | float | yes |
| sou_lineseq | smallint | yes |
| sou_ref | char(20) | yes |
| sou_secref | char(13) | yes |
| sou_poline | integer | yes |

---

## soclaim — Claims

Supplier claim records (rebate/deal claims against supplier invoices).

| Column | Type | Nulls |
|--------|------|-------|
| socl_supplier | char(10) | yes |
| socl_batch | char(6) | yes |
| socl_clstat | integer | yes |
| socl_customer | char(10) | yes |
| socl_rate | float | yes |
| socl_trandate | date | yes |
| socl_cltype | char(1) | yes |
| socl_lntype | char(1) | yes |
| socl_product | char(15) | yes |
| socl_qty | float | yes |
| socl_stloc | char(5) | yes |
| socl_recseq | smallint | yes |
| socl_cossal | float | yes |
| socl_claim | float | yes |
| socl_glclaim | float | yes |
| socl_suppcurr | char(4) | yes |
| socl_suppcost | float | yes |
| socl_sdqcost | float | yes |
| socl_sdqprice | float | yes |
| socl_ordref | char(8) | yes |
| socl_invref | char(8) | yes |
| socl_quotref | char(8) | yes |
| socl_supparef | char(15) | yes |
| socl_rpdate | date | yes |
| socl_csource | char(1) | yes |
| socl_suppprod | char(40) | yes |
| socl_sdcost | float | yes |
| socl_div | char(4) | yes |
| socl_company | char(4) | yes |
| socl_scomp | char(4) | yes |
| socl_ccomp | char(4) | yes |
| socl_crecomp | char(4) | yes |
| socl_suppclref | char(25) | yes |
| socl_suppcrdnt | char(25) | yes |
| socl_sdexpiry | date | yes |
| socl_procsupp | char(1) | yes |
| socl_seq | smallint | yes |
| socl_linseq | smallint | yes |

---

## soconfig — Configuration Items

Per-order configuration/component records (configured product lines).

| Column | Type | Nulls |
|--------|------|-------|
| socf_ordref | char(8) | yes |
| socf_ordline | integer | yes |
| socf_seq | integer | yes |
| socf_product | char(15) | yes |
| socf_qty | float | yes |
| socf_type | char(1) | yes |
| socf_sellpr | float | yes |
| socf_cost | float | yes |

---

## socons — Consignments

Consignment tracking records linking orders to carrier/delivery slots.

| Column | Type | Nulls |
|--------|------|-------|
| soco_consign | char(25) | yes |
| soco_ordref | char(8) | yes |
| soco_suffix | smallint | yes |
| soco_pikloc | char(5) | yes |
| soco_line | serial | no |
| soco_contract | char(10) | yes |
| soco_carser | char(10) | yes |
| soco_delref | char(8) | yes |
| soco_constat | char(8) | yes |
| soco_condate | date | yes |
| soco_contime | smallfloat | yes |
| soco_deldate | date | yes |
| soco_deltime | smallfloat | yes |
| soco_confirmed | char(1) | yes |
| soco_status | smallint | yes |
| soco_receiver | char(30) | yes |
| soco_colldate | date | yes |
| soco_colltime | smallfloat | yes |

---

## sodels — Delivery Scales / Rate Bands

Delivery charge rate bands by area/product group with up to 14 weight break tiers.

| Column | Type | Nulls |
|--------|------|-------|
| sodl_trcode | char(1) | yes |
| sodl_deldesc | char(30) | yes |
| sodl_pcode | char(40) | yes |
| sodl_area | char(4) | yes |
| sodl_pgroup | char(4) | yes |
| sodl_brk1 | float | yes |
| sodl_brk2 | float | yes |
| sodl_brk3 | float | yes |
| sodl_brk4 | float | yes |
| sodl_brk5 | float | yes |
| sodl_brk6 | float | yes |
| sodl_brk7 | float | yes |
| sodl_brk8 | float | yes |
| sodl_brk9 | float | yes |
| sodl_brk10 | float | yes |
| sodl_brk11 | float | yes |
| sodl_brk12 | float | yes |
| sodl_brk13 | float | yes |
| sodl_brk14 | float | yes |
| sodl_del1 | float | yes |
| sodl_del2 | float | yes |
| sodl_del3 | float | yes |
| sodl_del4 | float | yes |
| sodl_del5 | float | yes |
| sodl_del6 | float | yes |
| sodl_del7 | float | yes |
| sodl_del8 | float | yes |
| sodl_del9 | float | yes |
| sodl_del10 | float | yes |
| sodl_del11 | float | yes |
| sodl_del12 | float | yes |
| sodl_del13 | float | yes |
| sodl_del14 | float | yes |
| sodl_cost1 | float | yes |
| sodl_cost2 | float | yes |
| sodl_cost3 | float | yes |
| sodl_cost4 | float | yes |
| sodl_costs5 | float | yes |
| sodl_costs6 | float | yes |
| sodl_costs7 | float | yes |
| sodl_costs8 | float | yes |
| sodl_costs9 | float | yes |
| sodl_costs10 | float | yes |
| sodl_cost11 | float | yes |
| sodl_cost12 | float | yes |
| sodl_cost13 | float | yes |
| sodl_cost14 | float | yes |

---

## soiindex — Item Index

Lightweight index of products on an order (used for fast lookup).

| Column | Type | Nulls |
|--------|------|-------|
| soii_ordref | char(8) | yes |
| soii_seq | smallint | yes |
| soii_loc | char(5) | yes |
| soii_product | char(40) | yes |
| soii_status | char(1) | yes |

---

## soinvcod — Invoice Codes

Lookup table of invoice type codes and descriptions.

| Column | Type | Nulls |
|--------|------|-------|
| soic_invcode | char(4) | yes |
| soic_invdesc | char(30) | yes |

---

## soinvex — Invoice Exceptions / Plug Adjustments

Records adjustments or exceptions applied during invoice generation.

| Column | Type | Nulls |
|--------|------|-------|
| sox_proof | integer | yes |
| sox_seq | integer | yes |
| sox_invref | char(8) | yes |
| sox_ordref | char(8) | yes |
| sox_runtime | integer | yes |
| sox_opid | char(4) | yes |
| sox_reason | char(1) | yes |
| sox_txplg1 | char(40) | yes |
| sox_txplg2 | char(40) | yes |
| sox_nuplg1 | float | yes |
| sox_nuplg2 | float | yes |

---

## soload — Load / Route Records

Van load and route planning records.

| Column | Type | Nulls |
|--------|------|-------|
| sol_loadno | integer | yes |
| sol_desdate | date | yes |
| sol_routeno | smallint | yes |
| sol_vectype | integer | yes |
| sol_drvtype | integer | yes |
| sol_rlen | smallint | yes |
| sol_rname | char(8) | yes |
| sol_vname | char(8) | yes |
| sol_dname | char(16) | yes |
| sol_text1 | char(50) | yes |
| sol_text2 | char(50) | yes |
| sol_status | char(1) | yes |
| sol_stime | integer | yes |

---

## somast — Master Orders

Links master orders to sub-orders (blanket/call-off order relationships).

| Column | Type | Nulls |
|--------|------|-------|
| som_master | char(8) | yes |
| som_subord | char(8) | yes |
| som_customer | char(10) | yes |
| som_record | char(1) | yes |
| som_type | char(1) | yes |

---

## sopay — Order Payments

Payment records against a sales order (card, cash, BACS etc).

| Column | Type | Nulls |
|--------|------|-------|
| sopy_ordref | char(8) | yes |
| sopy_payref | char(8) | yes |
| sopy_method | char(8) | yes |
| sopy_cardnum | char(20) | yes |
| sopy_carddate | char(7) | yes |
| sopy_author | char(20) | yes |
| sopy_payval | float | yes |
| sopy_reference | char(15) | yes |
| sopy_issueno | smallint | yes |
| sopy_actdate | date | yes |
| sopy_status | char(1) | yes |
| sopy_customer | char(10) | yes |
| sopy_drbank | char(5) | yes |
| sopy_drbran | char(20) | yes |
| sopy_drname | char(40) | yes |
| sopy_acctref | char(10) | yes |
| sopy_batch | char(6) | yes |
| sopy_seq | serial | no |
| sopy_paycode | char(4) | yes |

---

## sopcodes — Promotion / Priority Codes

General code lookup (type + code + description). Used for various SO code fields.

| Column | Type | Nulls |
|--------|------|-------|
| soc_type | char(1) | yes |
| soc_code | char(10) | yes |
| soc_desc | char(40) | yes |

---

## sorecov — Recovery / Profitability Lines

Recovery/margin lines used for profitability calculations.

| Column | Type | Nulls |
|--------|------|-------|
| sore_ordref | char(8) | yes |
| sore_ordtype | char(1) | yes |
| sore_stopcode | char(1) | yes |
| sore_seq | smallint | yes |
| sore_product | char(15) | yes |
| sore_quantity | float | yes |
| sore_price | float | yes |
| sore_cossal | float | yes |
| sore_value | float | yes |
| sore_reqdate | date | yes |
| sore_profit | char(1) | yes |
| sore_margin | float | yes |
| sore_customer | char(10) | yes |
| sore_leasehld | char(1) | yes |
| sore_leasechhl | char(1) | yes |

---

## sosdhead — SD Quote Header

Supplier Direct (SD) quote/deal header records.

| Column | Type | Nulls |
|--------|------|-------|
| sosdh_quotref | char(8) | yes |
| sosdh_supplier | char(10) | yes |
| sosdh_customer | char(10) | yes |
| sosdh_status | char(1) | yes |
| sosdh_docreq | char(1) | yes |
| sosdh_suppqref | char(25) | yes |
| sosdh_supparef | char(15) | yes |
| sosdh_expiry | date | yes |
| sosdh_intproj | char(15) | yes |
| sosdh_extproj | char(15) | yes |
| sosdh_credate | date | yes |
| sosdh_opid | char(4) | yes |
| sosdh_comm1 | char(40) | yes |
| sosdh_comm2 | char(40) | yes |
| sosdh_vary | smallfloat | yes |
| sosdh_suppcurr | char(4) | yes |
| sosdh_edisdq | smallint | yes |
| sosdh_edisda | smallint | yes |
| sosdh_cond1 | char(1) | yes |
| sosdh_cond2 | char(1) | yes |
| sosdh_cond3 | char(1) | yes |
| sosdh_cond4 | char(1) | yes |
| sosdh_cond5 | char(1) | yes |
| sosdh_scomp | char(4) | yes |
| sosdh_ccomp | char(4) | yes |

---

## sosditem — SD Quote Line Items

Line items on a Supplier Direct quote. Links to sosdhead via sosdi_quotref.

| Column | Type | Nulls |
|--------|------|-------|
| sosdi_quotref | char(8) | yes |
| sosdi_product | char(40) | yes |
| sosdi_qqty | float | yes |
| sosdi_qcost | float | yes |
| sosdi_qprice | float | yes |
| sosdi_qglprice | float | yes |
| sosdi_shipqty | float | yes |
| sosdi_shipcost | float | yes |
| sosdi_shipprice | float | yes |
| sosdi_qclaimed | float | yes |
| sosdi_vclaimed | float | yes |
| sosdi_ncost | float | yes |
| sosdi_sprice | float | yes |
| sosdi_lnstat | char(1) | yes |
| sosdi_lntext | char(40) | yes |
| sosdi_resqty | float | yes |
| sosdi_extref | char(15) | yes |
| sosdi_margin | float | yes |
| sosdi_lineno | smallint | yes |

---

## soclink — Currency Link Pricing

Customer/product currency link records for foreign currency pricing.

| Column | Type | Nulls |
|--------|------|-------|
| sock_type | char(1) | yes |
| sock_customer | char(10) | yes |
| sock_pcode | char(15) | yes |
| sock_linkcurr | char(5) | yes |
| sock_cstbasis | float | yes |
| sock_salecurr | char(5) | yes |
| sock_linkrate | float | yes |
| sock_uplinkvar | float | yes |
| sock_lolinkvar | float | yes |

---

## sotcust — Temporary Customer Records

Temporary/transient customer address records (used during order entry).

| Column | Type | Nulls |
|--------|------|-------|
| sot_intern | char(10) | yes |
| sot_intdel | char(4) | yes |
| sot_exterc | char(22) | yes |
| sot_extdel | char(20) | yes |

---

## sovan — Van Schedule

Van scheduling records linking orders to van areas for route planning.

| Column | Type | Nulls |
|--------|------|-------|
| sov_vanarea | char(4) | yes |
| sov_ordref | char(8) | yes |
| sov_suffix | smallint | yes |
| sov_postcd | char(10) | yes |
| sov_weight | float | yes |
| sov_cubvol | float | yes |
| sov_stloc | char(5) | yes |
| sov_date | date | yes |
| sov_delref | char(8) | yes |

---

## sopara — System Parameters A

Main SOP system configuration parameters (single-row control table).

*(196 columns — see raw definition for full list. Key fields below.)*

| Column | Type | Nulls |
|--------|------|-------|
| sop_ordpre | char(4) | yes |
| sop_ordnum | integer | yes |
| sop_inpre | char(4) | yes |
| sop_invno | integer | yes |
| sop_crdpre | char(4) | yes |
| sop_crdno | integer | yes |
| sop_quotpre | char(4) | yes |
| sop_quotno | integer | yes |
| sop_retpre | char(4) | yes |
| sop_retno | integer | yes |
| sop_sdpre | char(4) | yes |
| sop_sdno | integer | yes |
| sop_nxtload | integer | yes |
| sop_nxtaudit | integer | yes |
| sop_nextseq | integer | yes |
| sop_hisper | smallint | yes |
| sop_bank | char(10) | yes |
| sop_dfltform | char(8) | yes |
| sop_dlvcode | char(40) | yes |
| sop_sdglacc | char(15) | yes |
| sop_ppglacc | char(15) | yes |
| sop_inuse | char(1) | yes |

---

## soparb — System Parameters B

Extended SOP configuration parameters (overflow from sopara, single-row).

*(109 columns — see raw definition for full list. Key fields below.)*

| Column | Type | Nulls |
|--------|------|-------|
| sopb_exptype | char(10) | yes |
| sopb_codcharge | char(15) | yes |
| sopb_misccost | char(15) | yes |
| sopb_alldays | smallint | yes |
| sopb_mastlim | smallint | yes |
| sopb_sallevel | smallint | yes |
| sopb_relperd | smallint | yes |
| sopb_refbank | char(10) | yes |
| sopb_refcard | char(16) | yes |
| sopb_workflow | char(1) | yes |

---

*Note: sopara and soparb are system configuration tables — not transactional. They will not appear in ER diagrams as they have no foreign key relationships.*
