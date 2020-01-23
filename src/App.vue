<template>
  <div id="app">
    <ejs-grid ref="grid"
      :dataSource="data"
      :allowPaging="true"
      :allowPdfExport="true"
      :allowExcelExport ="true"
      :pageSettings="pageSettings"
      :toolbar="toolbarOptions"
      :toolbarClick="gridExport">
      <e-columns>
        <e-column field="OrderID" headerText="Order ID" textAlign="Right"></e-column>
        <e-column field="CustomerID" headerText="Customer ID"></e-column>
        <e-column field="ShipCity" headerText="ShipCity"></e-column>
        <e-column field="ShipCountry" headerText="ShipCountry"></e-column>
      </e-columns>
    </ejs-grid>
  </div>
</template>

<script>

import Vue from "vue";
import { GridPlugin, Page, Toolbar, PdfExport, ExcelExport } from "@syncfusion/ej2-vue-grids";
import { data } from "./dataSource";

Vue.use(GridPlugin);

export default {
  data() {
    return {
      data: data,
      pageSettings:{ pageSize: 6 },
      toolbarOptions: ['PdfExport', 'ExcelExport']
    };
  },
  methods:{
    gridExport(args){
      var girdInst = this.$refs.grid;
      if(girdInst){
        if(args.item.id.includes('pdfexport')){
          girdInst.pdfExport({
            fileName: "invoice.pdf",
            exportType: "CurrentPage",
            theme: {
              header: {
                bold: true,
                fontName: "Calibri",
                fontSize: 10
              },
              record: {
                fontColor: "#0000ff",
                fontName: "Calibri",
                fontSize: 8
              }
            },
            header:{
              fromTop: 0,
              height: 130,
              contents: [{
                type: "Text",
                value: "Northwind Traders",
                position: { x: 0, y: 50 },
                style: { fontSize: 20 }
              }]
            },
            footer: {
              contents: [{
                type: "Text",
                value: "Thank You",
                position: { x: 0, y: 50 },
                style: { fontSize: 20 }
              }],
              fromBottom: 130,
              height: 130
            }
          });
        } else if(args.item.id.includes('excelexport')){
          girdInst.excelExport({
            fileName: "invoice.xlsx",
            exportType: "CurrentPage",
            theme: {
              header: {
                bold: true,
                fontName: "Calibri",
                fontSize: 10
              },
              record: {
                fontColor: "#0000ff",
                fontName: "Calibri",
                fontSize: 8
              }
            },
            header: {
              headerRows: 1,
              rows: [{
                cells: [{
                  colSpan: 4,
                  value: 'Northwind Traders',
                  style: { fontSize: 20, hAlign: 'Center', bold: true }
                }]
              }]
            },
            footer: {
              footerRows: 1,
              rows: [{
                cells: [{
                  colSpan: 4,
                  value: 'Thank You',
                  style: { fontSize: 20, hAlign: 'Center', bold: true }
                }]
              }]
            }
          })
        }
      }
    }
  },
  provide: {
    grid: [ Page, Toolbar, PdfExport, ExcelExport ]
  },
};
</script>

<style>
@import url("https://cdn.syncfusion.com/ej2/material.css");
</style>
