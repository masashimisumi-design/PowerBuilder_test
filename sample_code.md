```pb
$PBExportHeader$d_manifest_monthly_report.srd
$PBExportComments$月次マニフェスト管理・請求集計表（排出事業者別）
release 10.5;
datawindow(units=0 timer_interval=0 color=1073741824 processing=0 HTMLDW=no print.printername="" print.documentname="ManifestReport" print.orientation = 1 print.margin.left = 110 print.margin.right = 110 print.margin.top = 96 print.margin.bottom = 96 print.paper.source = 0 print.paper.size = 0 print.canavedit = yes print.prompt = no print.buttons = no print.preview.buttons = no print.cliptext = no print.overrideprintjob = no print.collate = yes )
header(height=220 color="536870912" )
header.1(height=84 color="536870912" )
detail(height=76 color="536870912" )
trailer.1(height=112 color="536870912" )
summary(height=140 color="536870912" )
footer(height=64 color="536870912" )
table(column=(type=char(10) updatewhereclause=yes name=customer_code dbname="t_manifest.gen_customer_code" )
 column=(type=char(60) updatewhereclause=no name=customer_name dbname="m_customer.customer_name1" )
 column=(type=char(15) updatewhereclause=yes name=manifest_no dbname="t_manifest.manifest_no" )
 column=(type=char(1) updatewhereclause=yes name=manifest_type dbname="t_manifest.manifest_type" values="紙	1/電子	2/" )
 column=(type=datetime updatewhereclause=yes name=issue_date dbname="t_manifest.issue_date" )
 column=(type=datetime updatewhereclause=yes name=disposal_date dbname="t_manifest.disposal_end_date" )
 column=(type=char(10) updatewhereclause=yes name=waste_code dbname="t_manifest.waste_item_code" )
 column=(type=char(40) updatewhereclause=no name=waste_name dbname="m_waste_item.item_name" )
 column=(type=char(20) updatewhereclause=yes name=hauler_name dbname="m_hauler.hauler_name" )
 column=(type=decimal(2) updatewhereclause=yes name=weight_kg dbname="t_manifest.weight_kg" )
 column=(type=decimal(2) updatewhereclause=yes name=unit_price dbname="t_manifest.unit_price" )
 column=(type=long updatewhereclause=yes name=amount dbname="t_manifest.amount" )
 column=(type=long updatewhereclause=yes name=tax_amount dbname="t_manifest.tax_amount" )
 column=(type=char(10) updatewhereclause=yes name=plant_code dbname="t_manifest.final_plant_code" )
 column=(type=char(40) updatewhereclause=no name=plant_name dbname="m_plant.plant_name" )
 retrieve="SELECT t_manifest.gen_customer_code,
    m_customer.customer_name1,
    t_manifest.manifest_no,
    t_manifest.manifest_type,
    t_manifest.issue_date,
    t_manifest.disposal_end_date,
    t_manifest.waste_item_code,
    m_waste_item.item_name,
    m_hauler.hauler_name,
    t_manifest.weight_kg,
    t_manifest.unit_price,
    t_manifest.amount,
    t_manifest.tax_amount,
    t_manifest.final_plant_code,
    m_plant.plant_name
 FROM t_manifest
    LEFT OUTER JOIN m_customer ON t_manifest.gen_customer_code = m_customer.customer_code
    LEFT OUTER JOIN m_waste_item ON t_manifest.waste_item_code = m_waste_item.item_code
    LEFT OUTER JOIN m_hauler ON t_manifest.hauler_code = m_hauler.hauler_code
    LEFT OUTER JOIN m_plant ON t_manifest.final_plant_code = m_plant.plant_code
 WHERE ( t_manifest.issue_date >= :dt_from ) AND
       ( t_manifest.issue_date <= :dt_to ) AND
       ( t_manifest.delete_flg = '0' )
 ORDER BY t_manifest.gen_customer_code ASC, t_manifest.issue_date ASC"
 arguments=(("dt_from", datetime),("dt_to", datetime)) )
group(name=group_customer by=("customer_code" ) newpage=yes )
text(band=header alignment="0" text="月次産業廃棄物管理・請求集計表" border="0" color="33554432" x="14" y="20" height="92" width="1200" html.valueishtml="0"  name=t_title visible="1"  font.face="ＭＳ Ｐゴシック" font.height="-16" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="1" text="作成日:" border="0" color="33554432" x="2500" y="32" height="64" width="200" html.valueishtml="0"  name=t_date_label visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
compute(band=header alignment="0" expression="Today()" border="0" color="33554432" x="2710" y="32" height="64" width="350" format="yyyy/mm/dd" html.valueishtml="0"  name=compute_today visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
line(band=header x1="10" y1="130" x2="3100" y2="130" pen.style="solid" pen.width="5" pen.color="33554432"  name=l_header_1 visible="1" )
text(band=header alignment="0" text="マニフェストNo" border="0" color="33554432" x="14" y="140" height="60" width="350" html.valueishtml="0"  name=t_h_manifest visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="0" text="交付日" border="0" color="33554432" x="380" y="140" height="60" width="250" html.valueishtml="0"  name=t_h_issue visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="0" text="廃棄物名" border="0" color="33554432" x="650" y="140" height="60" width="500" html.valueishtml="0"  name=t_h_waste visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="0" text="収集運搬業者" border="0" color="33554432" x="1170" y="140" height="60" width="400" html.valueishtml="0"  name=t_h_hauler visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="1" text="重量(kg)" border="0" color="33554432" x="1600" y="140" height="60" width="300" html.valueishtml="0"  name=t_h_weight visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="1" text="単価" border="0" color="33554432" x="1920" y="140" height="60" width="250" html.valueishtml="0"  name=t_h_price visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="1" text="金額(税抜)" border="0" color="33554432" x="2200" y="140" height="60" width="300" html.valueishtml="0"  name=t_h_amount visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header alignment="0" text="最終処分場" border="0" color="33554432" x="2550" y="140" height="60" width="500" html.valueishtml="0"  name=t_h_plant visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
text(band=header.1 alignment="0" text="排出事業者：" border="0" color="16711680" x="14" y="12" height="60" width="300" html.valueishtml="0"  name=t_grp_cust_lbl visible="1"  font.face="ＭＳ ゴシック" font.height="-10" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=header.1 id=1 alignment="0" tabsequence=0 border="0" color="0" x="320" y="12" height="60" width="200" format="[general]" html.valueishtml="0"  name=customer_code visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-10" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=header.1 id=2 alignment="0" tabsequence=0 border="0" color="0" x="540" y="12" height="60" width="1000" format="[general]" html.valueishtml="0"  name=customer_name visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-10" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=3 alignment="0" tabsequence=0 border="0" color="33554432" x="14" y="4" height="60" width="350" format="[general]" html.valueishtml="0"  name=manifest_no visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=5 alignment="0" tabsequence=0 border="0" color="33554432" x="380" y="4" height="60" width="250" format="yyyy/mm/dd" html.valueishtml="0"  name=issue_date visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=8 alignment="0" tabsequence=0 border="0" color="33554432" x="650" y="4" height="60" width="500" format="[general]" html.valueishtml="0"  name=waste_name visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=9 alignment="0" tabsequence=0 border="0" color="33554432" x="1170" y="4" height="60" width="400" format="[general]" html.valueishtml="0"  name=hauler_name visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=10 alignment="1" tabsequence=0 border="0" color="33554432" x="1600" y="4" height="60" width="300" format="#,##0.00" html.valueishtml="0"  name=weight_kg visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=11 alignment="1" tabsequence=0 border="0" color="33554432" x="1920" y="4" height="60" width="250" format="#,##0" html.valueishtml="0"  name=unit_price visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=12 alignment="1" tabsequence=0 border="0" color="33554432" x="2200" y="4" height="60" width="300" format="#,##0" html.valueishtml="0"  name=amount visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
column(band=detail id=15 alignment="0" tabsequence=0 border="0" color="33554432" x="2550" y="4" height="60" width="500" format="[general]" html.valueishtml="0"  name=plant_name visible="1" edit.limit=0 edit.case=any edit.focusrectangle=no edit.autoselect=yes  font.face="ＭＳ ゴシック" font.height="-9" font.weight="400"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
line(band=trailer.1 x1="10" y1="8" x2="3100" y2="8" pen.style="solid" pen.width="5" pen.color="33554432"  name=l_trailer_1 visible="1" )
text(band=trailer.1 alignment="0" text="【小計】" border="0" color="33554432" x="1200" y="20" height="60" width="200" html.valueishtml="0"  name=t_subtotal_lbl visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
compute(band=trailer.1 alignment="1" expression="sum(weight_kg for group 1)" border="0" color="33554432" x="1600" y="20" height="60" width="300" format="#,##0.00" html.valueishtml="0"  name=c_sum_weight_grp visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
compute(band=trailer.1 alignment="1" expression="sum(amount for group 1)" border="0" color="33554432" x="2200" y="20" height="60" width="300" format="#,##0" html.valueishtml="0"  name=c_sum_amount_grp visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
compute(band=trailer.1 alignment="1" expression="sum(tax_amount for group 1)" border="0" color="33554432" x="2550" y="20" height="60" width="300" format="#,##0" html.valueishtml="0"  name=c_sum_tax_grp visible="1"  font.face="ＭＳ ゴシック" font.height="-9" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
line(band=summary x1="10" y1="10" x2="3100" y2="10" pen.style="double" pen.width="15" pen.color="33554432"  name=l_summary_1 visible="1" )
text(band=summary alignment="0" text="【総合計】" border="0" color="33554432" x="1200" y="30" height="70" width="300" html.valueishtml="0"  name=t_grand_total_lbl visible="1"  font.face="ＭＳ Ｐゴシック" font.height="-11" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="536870912" )
compute(band=summary alignment="1" expression="sum(weight_kg for all)" border="2" color="33554432" x="1600" y="30" height="70" width="300" format="#,##0.00" html.valueishtml="0"  name=c_grand_weight visible="1"  font.face="ＭＳ ゴシック" font.height="-10" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.color="16777215" )
compute(band=summary alignment="1" expression="sum(amount for all)" border="2" color="33554432" x="2200" y="30" height="70" width="300" format="#,##0" html.valueishtml="0"  name=c_grand_amount visible="1"  font.face="ＭＳ ゴシック" font.height="-10" font.weight="700"  font.family="2" font.pitch="2" font.charset="128" background.mode="1" background.
```
