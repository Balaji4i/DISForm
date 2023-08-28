package view;

import com.view.utils.ADFUtils;
import com.view.utils.JSFUtils;

import java.math.BigDecimal;

import java.text.SimpleDateFormat;

import java.util.ArrayList;

import java.util.Date;

import javax.faces.context.FacesContext;
import javax.faces.event.ActionEvent;
import javax.faces.event.ValueChangeEvent;

import model.vo.DutyAllowance_VORowImpl;
import model.vo.XXSSHR_DIS_FORM_Hdr_VORowImpl;

import model.vo.XxsshrDisContingentLinesVORowImpl;

import oracle.adf.model.OperationBinding;
import oracle.adf.model.binding.DCIteratorBinding;
import oracle.adf.share.ADFContext;
import oracle.adf.view.rich.component.rich.data.RichTable;
import oracle.adf.view.rich.component.rich.input.RichSelectBooleanCheckbox;
import oracle.adf.view.rich.context.AdfFacesContext;

import oracle.jbo.Row;
import oracle.jbo.RowSetIterator;
import oracle.jbo.ViewCriteria;
import oracle.jbo.ViewCriteriaRow;
import oracle.jbo.ViewObject;

public class AddEditDisForm {
    private RichTable beneficiaryTab;
    private RichSelectBooleanCheckbox emerPrimaryContactFlag;
    private RichSelectBooleanCheckbox emerSecondaryContactFlag;
    private RichTable emergencytab;
    private RichTable contingentTable;
    private RichSelectBooleanCheckbox contiPrimaryContactFlag;
    private RichSelectBooleanCheckbox contiSecondaryContactFlag;

    public AddEditDisForm() {
    }


    public void onClickSave(ActionEvent actionEvent) {
        boolean result = false;
        ViewObject vo = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        XXSSHR_DIS_FORM_Hdr_VORowImpl hdrRow = (XXSSHR_DIS_FORM_Hdr_VORowImpl) vo.getCurrentRow();

        ViewObject disFormLinesVOO = ADFUtils.findIterator("XXSSHR_DIS_FORM_LINES_VOIterator").getViewObject();

        ViewObject disContiVO = ADFUtils.findIterator("XxsshrDisContingentLinesVOIterator").getViewObject();
        
        if (vo.getCurrentRow() != null){
            BigDecimal totProp =
                (vo.getCurrentRow().getAttribute("TotalProportion") == null ? new BigDecimal(0) :
                 (BigDecimal) vo.getCurrentRow().getAttribute("TotalProportion"));
            vo.getCurrentRow().setAttribute("TotalProportion", totProp);

            BigDecimal totContiProp =
                (vo.getCurrentRow().getAttribute("TotalContiProportion") == null ? new BigDecimal(0) :
                 (BigDecimal) vo.getCurrentRow().getAttribute("TotalContiProportion"));
            vo.getCurrentRow().setAttribute("TotalContiProportion", totContiProp);


            BigDecimal a = new BigDecimal(100);
            BigDecimal b = new BigDecimal(100);
            System.out.println("Total pro---- " + hdrRow.getTotalProportion());
            System.err.println(hdrRow.getTotalProportion().compareTo(a) == 1);
            System.err.println(hdrRow.getTotalProportion().compareTo(a) == 0);
            System.err.println(hdrRow.getTotalProportion().compareTo(a) == -1);
            if (disFormLinesVOO.getCurrentRow() != null && (hdrRow.getTotalProportion().compareTo(a) == 1)) {
                System.out.println("Inside if loop");
                JSFUtils.addFacesErrorMessage("Total Primary Beneficiary Proportion should not be Greater than 100%");
            } else if (disContiVO.getCurrentRow() != null && (hdrRow.getTotalContiProportion().compareTo(b) == 1)) {
                System.out.println("Inside if loop");
                JSFUtils.addFacesErrorMessage("Total Contingent Beneficiary Proportion should not be Greater than 100%");

            } else {
                    System.out.println("Inside else loop");
                hdrRow.setApprovalStatus("DRAFT");
                hdrRow.setTotalProportion(hdrRow.getTotalProportion());
                ADFUtils.findOperation("Commit").execute();
                JSFUtils.addFacesInformationMessage("API Form Saved Successfully!!");
            } 
        }
       

    }

    public void onClickCancel(ActionEvent actionEvent) {
        ViewObject HdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        HdrVO.applyViewCriteria(null);
        HdrVO.executeQuery();
        ADFUtils.findOperation("Rollback").execute();
    }

    public void setOrgId() {
        Object obj = ADFContext.getCurrent()
                               .getSessionScope()
                               .get("personId");
        ViewObject LineVo =
            ADFUtils.getApplicationModuleForDataControl("Oando_AMDataControl").findViewObject("Employee_View_ROVO");
        ViewCriteria viewCriteria = LineVo.createViewCriteria();
        ViewCriteriaRow viewCriteriaRow = viewCriteria.createViewCriteriaRow();
        viewCriteriaRow.setAttribute("PersonId", obj);
        viewCriteria.addRow(viewCriteriaRow);
        LineVo.applyViewCriteria(viewCriteria);
        LineVo.executeQuery();
        System.out.println("LineVo Query ----" + LineVo.getQuery());
        System.out.println("Person Id ----" + obj);

        if (LineVo.getEstimatedRowCount() > 0) {
            Row row = LineVo.first();
            row.getAttribute("BusinessUnitId");
            row.getAttribute("PersonNumber");
            row.getAttribute("FullName");
            row.getAttribute("EmailAddress");
            row.getAttribute("BusinessUnitName");
            row.getAttribute("Cadre");
            System.out.println(row.getAttribute("PersonNumber"));
            System.out.println(row.getAttribute("FullName"));
            System.out.println(row.getAttribute("EmailAddress"));
            System.out.println(row.getAttribute("BusinessUnitName"));
            Object orgObj = row.getAttribute("BusinessUnitId");
            ADFContext.getCurrent()
                      .getSessionScope()
                      .put("orgId", orgObj);


            System.out.println("111111111");
            ViewObject DutyVo =
                ADFUtils.getApplicationModuleForDataControl("Oando_AMDataControl")
                .findViewObject("XXSSHR_DIS_FORM_Hdr_VO");
            Row r = DutyVo.first();
            Row newRow = DutyVo.createRow();
            newRow.setAttribute("PersonId", obj);
            newRow.setAttribute("Name_Trans", row.getAttribute("FullName"));
            newRow.setAttribute("Number_Trans", row.getAttribute("PersonNumber"));
            newRow.setAttribute("Email_Trans", row.getAttribute("EmailAddress"));
            newRow.setAttribute("Group_Trans", row.getAttribute("BusinessUnitName"));
            newRow.setAttribute("BusinessUnitId", row.getAttribute("BusinessUnitId"));
            newRow.setAttribute("Trans_Cadre", row.getAttribute("Cadre"));
            DutyVo.insertRow(newRow);
        }

    }

    public String onClickSubmit(ActionEvent actionEvent) {
        return null;
        //        boolean value = false;
        //        ViewObject disFormHdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        //        // ViewObject customerVo = ADFUtils.findIterator("XXSSHR_DIS_FORM_LINES_VOIterator").getViewObject();
        //        //RowSetIterator dtlsRS = customerVo.createRowSetIterator(null);
        //        int i = 0;
        //        //        while (dtlsRS.hasNext()) {
        //        //            Row r = dtlsRS.next();
        //        //            System.err.println("submit PrimaryFlag--" + r.getAttribute("PrimaryContactFlag"));
        //        //            if (r.getAttribute("PrimaryContactFlag") == "Y") {
        //        //                System.err.println("sub Current row");
        //        //                i++;
        //        //                continue;
        //        //            }
        //        //        }
        //
        //        ViewObject vo = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        //        XXSSHR_DIS_FORM_Hdr_VORowImpl hdrRow = (XXSSHR_DIS_FORM_Hdr_VORowImpl) vo.getCurrentRow();
        //        BigDecimal totProp =
        //            (vo.getCurrentRow().getAttribute("TotalProportion") == null ? new BigDecimal(0) :
        //             (BigDecimal) vo.getCurrentRow().getAttribute("TotalProportion"));
        //        vo.getCurrentRow().setAttribute("TotalProportion", totProp);
        //        System.out.println("Total propp---- " + hdrRow.getTotalProportion());
        //        BigDecimal defValue = new BigDecimal(100);
        //        if (hdrRow.getTotalProportion().compareTo(defValue) == 1 &&
        //            !(hdrRow.getTotalProportion().compareTo(defValue) == 0)) {
        //            System.out.println("Inside if loop");
        //            JSFUtils.addFacesErrorMessage("Total Proportion should be equal to 100%");
        //        } else {
        //
        //            String xmlData = null;
        //            String[] a = null;
        //            String disFormWSDL = null;
        //            disFormWSDL = ApprovalPayload.DIS_FORM_WSDL;
        //
        //
        //            XXSSHR_DIS_FORM_Hdr_VORowImpl disFormHdrRowImpl =
        //                (XXSSHR_DIS_FORM_Hdr_VORowImpl) disFormHdrVO.getCurrentRow();
        //
        //            String p_EmployeeName =
        //                disFormHdrVO.getCurrentRow().getAttribute("Name_Trans") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                        .getAttribute("Name_Trans")
        //                                                                                                                        .toString();
        //            String p_EmployeeNumber =
        //                disFormHdrVO.getCurrentRow().getAttribute("Number_Trans") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                            .getAttribute("Number_Trans")
        //                                                                                                                            .toString();
        //
        //            String p_Email =
        //                disFormHdrVO.getCurrentRow().getAttribute("Email_Trans") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                  .getAttribute("Email_Trans")
        //                                                                                                                  .toString();
        //
        //            String p_BusinessGroup =
        //                disFormHdrVO.getCurrentRow().getAttribute("Group_Trans") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                          .getAttribute("Group_Trans")
        //                                                                                                                          .toString();
        //
        //            String p_Cadre =
        //                disFormHdrVO.getCurrentRow().getAttribute("Trans_Cadre") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                  .getAttribute("Trans_Cadre")
        //                                                                                                                  .toString();
        //
        //            String p_DisFormID =
        //                disFormHdrVO.getCurrentRow().getAttribute("DisFormId") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                    .getAttribute("DisFormId")
        //                                                                                                                    .toString();
        //
        //
        //            String p_DisFormNo =
        //                disFormHdrVO.getCurrentRow().getAttribute("DisFormNo") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                    .getAttribute("DisFormNo")
        //                                                                                                                    .toString();
        //
        //            String p_PersonId =
        //                disFormHdrVO.getCurrentRow().getAttribute("PersonId") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                  .getAttribute("PersonId")
        //                                                                                                                  .toString();
        //
        //            String p_BusinessUnitId =
        //                disFormHdrVO.getCurrentRow().getAttribute("BusinessUnitId") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                              .getAttribute("BusinessUnitId")
        //                                                                                                                              .toString();
        //
        //            String p_TransDate =
        //                disFormHdrVO.getCurrentRow().getAttribute("TransactionDate") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                          .getAttribute("TransactionDate")
        //                                                                                                                          .toString();
        //
        //            String p_TotalProportion =
        //                disFormHdrVO.getCurrentRow().getAttribute("TotalProportion") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                                .getAttribute("TotalProportion")
        //                                                                                                                                .toString();
        //            String p_ApprovalStatus =
        //                disFormHdrVO.getCurrentRow().getAttribute("ApprovalStatus") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                              .getAttribute("ApprovalStatus")
        //                                                                                                                              .toString();
        //
        //            String p_Comments =
        //                disFormHdrVO.getCurrentRow().getAttribute("Comments") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                  .getAttribute("Comments")
        //                                                                                                                  .toString();
        //
        //            String p_ApproverComments =
        //                disFormHdrVO.getCurrentRow().getAttribute("ApproverComments") == null ? " " :
        //                disFormHdrVO.getCurrentRow()
        //                                                                                                                                  .getAttribute("ApproverComments")
        //                                                                                                                                  .toString();
        //
        //
        //            ArrayList<String> p_DisFormLineId = new ArrayList<String>();
        //            ArrayList<String> p_DisFormId = new ArrayList<String>();
        //            ArrayList<String> p_RelationshipType = new ArrayList<String>();
        //            ArrayList<String> p_FullName = new ArrayList<String>();
        //            ArrayList<String> p_Proportion = new ArrayList<String>();
        //            ArrayList<String> p_PrimaryContactFlag = new ArrayList<String>();
        //            ArrayList<String> p_SecondaryContactFlag = new ArrayList<String>();
        //            ArrayList<String> p_MobileNumber = new ArrayList<String>();
        //
        //            ViewObject disFormLinesVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_LINES_VOIterator").getViewObject();
        //            RowSetIterator rs = disFormLinesVO.createRowSetIterator(null);
        //            while (rs.hasNext()) {
        //                Row r = rs.next();
        //                p_DisFormLineId.add(r.getAttribute("DisFormLineId") == null ? " " :
        //                                    r.getAttribute("DisFormLineId").toString());
        //
        //                p_DisFormId.add(r.getAttribute("DisFormId") == null ? " " : r.getAttribute("DisFormId").toString());
        //                p_RelationshipType.add(r.getAttribute("RelationshipType") == null ? " " :
        //                                       r.getAttribute("RelationshipType").toString());
        //                p_FullName.add(r.getAttribute("FullName") == null ? " " : r.getAttribute("FullName").toString());
        //                p_Proportion.add(r.getAttribute("Proportion") == null ? " " : r.getAttribute("Proportion").toString());
        //                p_PrimaryContactFlag.add(r.getAttribute("PrimaryContactFlag") == null ? " " :
        //                                         r.getAttribute("PrimaryContactFlag").toString());
        //                p_SecondaryContactFlag.add(r.getAttribute("SecondaryContactFlag") == null ? " " :
        //                                           r.getAttribute("SecondaryContactFlag").toString());
        //                p_MobileNumber.add(r.getAttribute("MobileNo") == null ? " " : r.getAttribute("MobileNo").toString());
        //
        //            }
        //            rs.closeRowSetIterator();
        //
        //            // Decalring the variables for emergency loop
        //
        //            ArrayList<String> p_DisEmerContactId = new ArrayList<String>();
        //            // ArrayList<String> p_DisFormId = new ArrayList<String>();
        //            ArrayList<String> p_EmerRelationshipType = new ArrayList<String>();
        //            ArrayList<String> p_EmerFullName = new ArrayList<String>();
        //            ArrayList<String> p_EmerMobileNumber = new ArrayList<String>();
        //            ArrayList<String> p_EmerPrimaryContactFlag = new ArrayList<String>();
        //            ArrayList<String> p_EmerSecondaryContactFlag = new ArrayList<String>();
        //
        //
        //            ViewObject disFormEmerVO = ADFUtils.findIterator("XXSSHR_DIS_EMERGENCY_DETAILS_VOIterator").getViewObject();
        //
        //            RowSetIterator rsIter = disFormEmerVO.createRowSetIterator(null);
        //            while (rsIter.hasNext()) {
        //                Row r = rsIter.next();
        //                p_DisEmerContactId.add(r.getAttribute("DisEmerContactId") == null ? " " :
        //                                       r.getAttribute("DisEmerContactId").toString());
        //
        //                //p_DisFormId.add(r.getAttribute("DisFormId") == null ? " " : r.getAttribute("DisFormId").toString());
        //                p_EmerRelationshipType.add(r.getAttribute("EmerRelationshipType") == null ? " " :
        //                                           r.getAttribute("EmerRelationshipType").toString());
        //                p_EmerFullName.add(r.getAttribute("EmerFullName") == null ? " " :
        //                                   r.getAttribute("EmerFullName").toString());
        //                p_EmerMobileNumber.add(r.getAttribute("EmerMobileNo") == null ? " " :
        //                                       r.getAttribute("EmerMobileNo").toString());
        //                p_EmerPrimaryContactFlag.add(r.getAttribute("EmerPrimaryContactFlag") == null ? " " :
        //                                             r.getAttribute("EmerPrimaryContactFlag").toString());
        //                p_EmerSecondaryContactFlag.add(r.getAttribute("EmerSecondaryContactFlag") == null ? " " :
        //                                               r.getAttribute("EmerSecondaryContactFlag").toString());
        //
        //            }
        //            rs.closeRowSetIterator();
        //
        //            xmlData =
        //                ApprovalPayload.businessTypeXMLData(p_EmployeeName, p_EmployeeNumber, p_Email, p_BusinessGroup, p_Cadre,
        //                                                    p_DisFormID, p_DisFormNo, p_PersonId, p_BusinessUnitId, p_TransDate,
        //                                                    p_TotalProportion, p_ApprovalStatus, p_Comments, p_ApproverComments,
        //                                                    p_DisFormLineId, p_DisFormId, p_RelationshipType, p_FullName,
        //                                                    p_Proportion, p_PrimaryContactFlag, p_SecondaryContactFlag,
        //                                                    p_MobileNumber, p_MobileNumber1, p_EmailAddress ,p_ResiAddress,
        //                                                    p_DisEmerContactId, p_EmerRelationshipType,
        //                                                    p_EmerFullName, p_EmerMobileNumber, p_EmerPrimaryContactFlag,
        //                                                    p_EmerSecondaryContactFlag);
        //
        //            System.err.println("xmlData =>" + xmlData);
        //
        //            a = ApprovalProcess.invokeWsdl(xmlData, disFormWSDL, ApprovalPayload.DIS_FORM_METHOD);
        //            if (a[0] != null && a[0].equals("True")) {
        //                if (disFormHdrRowImpl != null) {
        //                    disFormHdrRowImpl.setApprovalStatus("SUBMITTED FOR APPROVAL");
        //                    OperationBinding binding = (OperationBinding) ADFUtils.findOperation("Commit").execute();
        //                }
        //                JSFUtils.addFacesInformationMessage("DIS Form Submitted Successfully");
        //                value = true;
        //            } else {
        //                JSFUtils.addFacesInformationMessage("Error");
        //                disFormHdrRowImpl.setApprovalStatus("DRAFT");
        //
        //            }
        //
        //        }
        //
        //        if (value) {
        //            disFormHdrVO.applyViewCriteria(null);
        //            disFormHdrVO.executeQuery();
        //            return "back";
        //        } else {
        //            return null;
        //
        //        }

        //        else {
        //            JSFUtils.addFacesErrorMessage("Atleast one Primary Contact should be selected. Please Select.");
        //        }
    }


    public void onClickPrimaryFlag(ValueChangeEvent valueChangeEvent) {
        valueChangeEvent.getComponent().processUpdates(FacesContext.getCurrentInstance());
        ViewObject customerVo = ADFUtils.findIterator("XXSSHR_DIS_FORM_LINES_VOIterator").getViewObject();
        RowSetIterator dtlsRS = customerVo.createRowSetIterator(null);
        int currIndex = customerVo.getCurrentRowIndex();
        int i = 0;
        while (dtlsRS.hasNext()) {
            Row r = dtlsRS.next();
            System.err.println("PrimaryFlag--" + r.getAttribute("PrimaryContactFlag"));
            if (i == currIndex) {
                System.err.println("Current row");
                i++;
                continue;
            }
            System.err.println("set false");
            r.setAttribute("PrimaryContactFlag", "N");
            i++;
        }
        AdfFacesContext.getCurrentInstance().addPartialTarget(beneficiaryTab);

    }

    public void setBeneficiaryTab(RichTable beneficiaryTab) {
        this.beneficiaryTab = beneficiaryTab;
    }

    public RichTable getBeneficiaryTab() {
        return beneficiaryTab;
    }

    public String onClickSubmitAction() {
        boolean value = false;
        boolean result = false;
        ViewObject disFormHdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        ViewObject disFormEmerVO = ADFUtils.findIterator("XXSSHR_DIS_EMERGENCY_DETAILS_VOIterator").getViewObject();
        ViewObject disFormLinesVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_LINES_VOIterator").getViewObject();
        ViewObject disFormContiVO = ADFUtils.findIterator("XxsshrDisContingentLinesVOIterator").getViewObject();
        RowSetIterator emerFormRS = disFormEmerVO.createRowSetIterator(null);
        int i = 0;
        int j = 0;
        //       // int a = 0;
        //        int b = 0;
        //        int c = 0;
        //        int d = 0;
        //        int s = 0;
        while (emerFormRS.hasNext()) {
            System.out.println("sub Emerg Current row");
            Row r = emerFormRS.next();
            // System.out.println("submit  Emerg PrimaryFlag--" + r.getAttribute("EmerPrimaryContactFlag"));
            if (r.getAttribute("EmerPrimaryContactFlag").equals("Y")) {
                // System.out.println("Emer Relation ship ----- " + r.getAttribute("EmerRelationshipType"));

                i++;
                //System.out.println("I Plues value is ------- " + i);
                continue;
            }
        }


        //        if (a != 0) {
        //            JSFUtils.addFacesErrorMessage("Please Enter the Proposed Travel Date ");
        //            result = true;
        //        }


        if (i > 0) {
            System.out.println("Into If loop ------");
            ViewObject vo = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
            XXSSHR_DIS_FORM_Hdr_VORowImpl hdrRow = (XXSSHR_DIS_FORM_Hdr_VORowImpl) vo.getCurrentRow();
            ViewObject disContiVO = ADFUtils.findIterator("XxsshrDisContingentLinesVOIterator").getViewObject();
            if(vo.getCurrentRow() != null){
                BigDecimal totProp =
                    (vo.getCurrentRow().getAttribute("TotalProportion") == null ? new BigDecimal(0) :
                     (BigDecimal) vo.getCurrentRow().getAttribute("TotalProportion"));
                vo.getCurrentRow().setAttribute("TotalProportion", totProp);

                BigDecimal totContiProp =
                    (vo.getCurrentRow().getAttribute("TotalContiProportion") == null ? new BigDecimal(0) :
                     (BigDecimal) vo.getCurrentRow().getAttribute("TotalContiProportion"));
                vo.getCurrentRow().setAttribute("TotalContiProportion", totContiProp);

            }
           
            BigDecimal defValue = new BigDecimal(100);
            BigDecimal defValue1 = new BigDecimal(100);
            if ((hdrRow.getTotalProportion().compareTo(defValue) == 1 ||
                 hdrRow.getTotalProportion().compareTo(defValue) == -1) &&
                !(hdrRow.getTotalProportion().compareTo(defValue) == 0) && vo.getEstimatedRowCount() > 0) {
                // System.out.println("Inside if loop");
                JSFUtils.addFacesErrorMessage("Total Primary Beneficiary Proportion should be equal to 100%");
            } else if ((hdrRow.getTotalContiProportion().compareTo(defValue1) == 1 ||
                        hdrRow.getTotalContiProportion().compareTo(defValue1) == -1) &&
                       !(hdrRow.getTotalContiProportion().compareTo(defValue1) == 0) &&
                       disContiVO.getEstimatedRowCount() > 0) {
                // System.out.println("Inside if loop");
                JSFUtils.addFacesErrorMessage("Total Contingent Beneficiary Proportion should be equal to 100%");
            } else if (disFormLinesVO.getCurrentRow()
                                     .getAttribute("DisBeneFlag")
                                     .equals("N")) {
                System.out.println("Into first else if  loop");
                JSFUtils.addFacesErrorMessage("Please select Group Life Insurance Beneficiary check box");

            } else if (disFormEmerVO.getCurrentRow()
                                    .getAttribute("DisEmerFlag")
                                    .equals("N")) {
                System.out.println("Into first else if  loop");
                JSFUtils.addFacesErrorMessage("Please select Emergency Contact check box");

            } else if (disFormHdrVO.getCurrentRow()
                                   .getAttribute("DisConfirmFlag")
                                   .equals("N")) {
                System.out.println("Into second else if  loop");
                JSFUtils.addFacesErrorMessage("Please select Data Protection check box");

            } else if (disFormHdrVO.getCurrentRow()
                                   .getAttribute("DisUnderstandFlag")
                                   .equals("N")) {
                System.out.println("Into third else if  loop");
                JSFUtils.addFacesErrorMessage("Please select Understand check box");

            } else if (disFormEmerVO.getEstimatedRowCount() < 2) {
                System.out.println("Into third else if  loop");
                JSFUtils.addFacesErrorMessage("Please provide atleast two Emergency contacts");
            } else {
                String xmlData = null;
                String[] a = null;
                String disFormWSDL = null;
                disFormWSDL = ApprovalPayload.DIS_FORM_WSDL;


                XXSSHR_DIS_FORM_Hdr_VORowImpl disFormHdrRowImpl =
                    (XXSSHR_DIS_FORM_Hdr_VORowImpl) disFormHdrVO.getCurrentRow();

                if (disFormHdrRowImpl != null) {
                    disFormHdrRowImpl.setApprovalStatus("SUBMITTED");
                }

                String p_EmployeeName =
                    disFormHdrVO.getCurrentRow().getAttribute("Name_Trans") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                            .getAttribute("Name_Trans")
                                                                                                                            .toString();
                String p_EmployeeNumber =
                    disFormHdrVO.getCurrentRow().getAttribute("Number_Trans") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                                .getAttribute("Number_Trans")
                                                                                                                                .toString();

                String p_Email =
                    disFormHdrVO.getCurrentRow().getAttribute("Email_Trans") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                      .getAttribute("Email_Trans")
                                                                                                                      .toString();

                String p_BusinessGroup =
                    disFormHdrVO.getCurrentRow().getAttribute("Group_Trans") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                              .getAttribute("Group_Trans")
                                                                                                                              .toString();

                String p_Cadre =
                    disFormHdrVO.getCurrentRow().getAttribute("Trans_Cadre") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                      .getAttribute("Trans_Cadre")
                                                                                                                      .toString();

                String p_DisFormID =
                    disFormHdrVO.getCurrentRow().getAttribute("DisFormId") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                        .getAttribute("DisFormId")
                                                                                                                        .toString();


                String p_DisFormNo =
                    disFormHdrVO.getCurrentRow().getAttribute("DisFormNo") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                        .getAttribute("DisFormNo")
                                                                                                                        .toString();

                String p_PersonId =
                    disFormHdrVO.getCurrentRow().getAttribute("PersonId") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                      .getAttribute("PersonId")
                                                                                                                      .toString();

                String p_BusinessUnitId =
                    disFormHdrVO.getCurrentRow().getAttribute("BusinessUnitId") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                                  .getAttribute("BusinessUnitId")
                                                                                                                                  .toString();

                String p_TransDate =
                    disFormHdrVO.getCurrentRow().getAttribute("TransactionDate") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                              .getAttribute("TransactionDate")
                                                                                                                              .toString();

                String p_TotalProportion =
                    disFormHdrVO.getCurrentRow().getAttribute("TotalProportion") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                                    .getAttribute("TotalProportion")
                                                                                                                                    .toString();
                String p_ApprovalStatus =
                    disFormHdrVO.getCurrentRow().getAttribute("ApprovalStatus") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                                  .getAttribute("ApprovalStatus")
                                                                                                                                  .toString();

                String p_Comments =
                    disFormHdrVO.getCurrentRow().getAttribute("Comments") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                      .getAttribute("Comments")
                                                                                                                      .toString();

                String p_ApproverComments =
                    disFormHdrVO.getCurrentRow().getAttribute("ApproverComments") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                              .getAttribute("ApproverComments")
                                                                                                              .toString();

                String p_TotalContiProportion =
                    disFormHdrVO.getCurrentRow().getAttribute("TotalContiProportion") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                  .getAttribute("TotalContiProportion")
                                                                                                                  .toString();


                String p_DisConfirmFlag =
                    disFormHdrVO.getCurrentRow().getAttribute("DisConfirmFlag") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                                                  .getAttribute("DisConfirmFlag")
                                                                                                                                  .toString();


                String p_DisUnderstandFlag =
                    disFormHdrVO.getCurrentRow().getAttribute("DisUnderstandFlag") == null ? " " :
                    disFormHdrVO.getCurrentRow()
                                                                                                               .getAttribute("DisUnderstandFlag")
                                                                                                               .toString();
                ArrayList<String> p_DisFormLineId = new ArrayList<String>();
                ArrayList<String> p_DisFormId = new ArrayList<String>();
                ArrayList<String> p_RelationshipType = new ArrayList<String>();
                ArrayList<String> p_FullName = new ArrayList<String>();
                ArrayList<String> p_Proportion = new ArrayList<String>();
                ArrayList<String> p_PrimaryContactFlag = new ArrayList<String>();
                ArrayList<String> p_SecondaryContactFlag = new ArrayList<String>();
                ArrayList<String> p_MobileNumber = new ArrayList<String>();
                ArrayList<String> p_MobileNumber1 = new ArrayList<String>();
                ArrayList<String> p_EmailAddress = new ArrayList<String>();
                ArrayList<String> p_ResiAddress = new ArrayList<String>();
                ArrayList<String> p_DisBeneFlag = new ArrayList<String>();


                RowSetIterator rs = disFormLinesVO.createRowSetIterator(null);
                while (rs.hasNext()) {
                    Row r = rs.next();
                    p_DisFormLineId.add(r.getAttribute("DisFormLineId") == null ? " " :
                                        r.getAttribute("DisFormLineId").toString());

                    p_DisFormId.add(r.getAttribute("DisFormId") == null ? " " : r.getAttribute("DisFormId").toString());
                    p_RelationshipType.add(r.getAttribute("RelationshipType") == null ? " " :
                                           r.getAttribute("RelationshipType").toString());
                    p_FullName.add(r.getAttribute("FullName") == null ? " " : r.getAttribute("FullName").toString());
                    p_Proportion.add(r.getAttribute("Proportion") == null ? " " :
                                     r.getAttribute("Proportion").toString());
                    p_PrimaryContactFlag.add(r.getAttribute("PrimaryContactFlag") == null ? " " :
                                             r.getAttribute("PrimaryContactFlag").toString());
                    p_SecondaryContactFlag.add(r.getAttribute("SecondaryContactFlag") == null ? " " :
                                               r.getAttribute("SecondaryContactFlag").toString());
                    p_MobileNumber.add(r.getAttribute("MobileNo") == null ? " " :
                                       r.getAttribute("MobileNo").toString());
                    p_MobileNumber1.add(r.getAttribute("MobileNo1") == null ? " " :
                                        r.getAttribute("MobileNo1").toString());
                    p_EmailAddress.add(r.getAttribute("EmailAddress") == null ? " " :
                                       r.getAttribute("EmailAddress").toString());
                    p_ResiAddress.add(r.getAttribute("ResiAddress") == null ? " " :
                                      r.getAttribute("ResiAddress").toString());
                    p_DisBeneFlag.add(r.getAttribute("DisBeneFlag") == null ? " " :
                                      r.getAttribute("DisBeneFlag").toString());

                }
                rs.closeRowSetIterator();

                // Decalring the variables for emergency loop

                ArrayList<String> p_DisEmerContactId = new ArrayList<String>();
                ArrayList<String> p_EmerDisFormId = new ArrayList<String>();
                ArrayList<String> p_EmerRelationshipType = new ArrayList<String>();
                ArrayList<String> p_EmerFullName = new ArrayList<String>();
                ArrayList<String> p_EmerMobileNumber = new ArrayList<String>();
                ArrayList<String> p_EmerPrimaryContactFlag = new ArrayList<String>();
                ArrayList<String> p_EmerSecondaryContactFlag = new ArrayList<String>();
                ArrayList<String> p_DisEmerFlag = new ArrayList<String>();

                RowSetIterator rsIter = disFormEmerVO.createRowSetIterator(null);
                while (rsIter.hasNext()) {
                    Row r = rsIter.next();
                    p_DisEmerContactId.add(r.getAttribute("DisEmerContactId") == null ? " " :
                                           r.getAttribute("DisEmerContactId").toString());

                    p_EmerDisFormId.add(r.getAttribute("DisFormId") == null ? " " :
                                        r.getAttribute("DisFormId").toString());
                    p_EmerRelationshipType.add(r.getAttribute("EmerRelationshipType") == null ? " " :
                                               r.getAttribute("EmerRelationshipType").toString());
                    p_EmerFullName.add(r.getAttribute("EmerFullName") == null ? " " :
                                       r.getAttribute("EmerFullName").toString());
                    p_EmerMobileNumber.add(r.getAttribute("EmerMobileNo") == null ? " " :
                                           r.getAttribute("EmerMobileNo").toString());
                    p_EmerPrimaryContactFlag.add(r.getAttribute("EmerPrimaryContactFlag") == null ? " " :
                                                 r.getAttribute("EmerPrimaryContactFlag").toString());
                    p_EmerSecondaryContactFlag.add(r.getAttribute("EmerSecondaryContactFlag") == null ? " " :
                                                   r.getAttribute("EmerSecondaryContactFlag").toString());
                    p_DisEmerFlag.add(r.getAttribute("DisEmerFlag") == null ? " " :
                                      r.getAttribute("DisEmerFlag").toString());

                }
                rs.closeRowSetIterator();

                ArrayList<String> p_DisContingentId = new ArrayList<String>();
                ArrayList<String> p_ContiDisFormId = new ArrayList<String>();
                ArrayList<String> p_ContiRelationshipType = new ArrayList<String>();
                ArrayList<String> p_ContiFullName = new ArrayList<String>();
                ArrayList<String> p_ContiProportion = new ArrayList<String>();
                ArrayList<String> p_ContiMobileNumber = new ArrayList<String>();
                ArrayList<String> p_ContiMobileNumber1 = new ArrayList<String>();
                ArrayList<String> p_ContiEmailAddress = new ArrayList<String>();
                ArrayList<String> p_ContiResiAddress = new ArrayList<String>();


                RowSetIterator rsItr = disFormContiVO.createRowSetIterator(null);
                while (rsItr.hasNext()) {
                    Row row = rsItr.next();
                    p_DisContingentId.add(row.getAttribute("DisContingentId") == null ? " " :
                                          row.getAttribute("DisContingentId").toString());

                    p_ContiDisFormId.add(row.getAttribute("DisFormId") == null ? " " :
                                         row.getAttribute("DisFormId").toString());
                    p_ContiRelationshipType.add(row.getAttribute("ContiRelationshipType") == null ? " " :
                                                row.getAttribute("ContiRelationshipType").toString());
                    p_ContiFullName.add(row.getAttribute("ContiFullName") == null ? " " :
                                        row.getAttribute("ContiFullName").toString());
                    p_ContiProportion.add(row.getAttribute("ContiProportion") == null ? " " :
                                          row.getAttribute("ContiProportion").toString());
                    p_ContiMobileNumber.add(row.getAttribute("ContiMobileNo") == null ? " " :
                                            row.getAttribute("ContiMobileNo").toString());
                    p_ContiMobileNumber1.add(row.getAttribute("ContiMobileNo1") == null ? " " :
                                             row.getAttribute("ContiMobileNo1").toString());
                    p_ContiEmailAddress.add(row.getAttribute("ContiEmailAddress") == null ? " " :
                                            row.getAttribute("ContiEmailAddress").toString());
                    p_ContiResiAddress.add(row.getAttribute("ContiResiAddress") == null ? " " :
                                           row.getAttribute("ContiResiAddress").toString());

                }
                rs.closeRowSetIterator();


                xmlData =
                    ApprovalPayload.businessTypeXMLData(p_EmployeeName, p_EmployeeNumber, p_Email, p_BusinessGroup,
                                                        p_Cadre, p_DisFormID, p_DisFormNo, p_PersonId, p_BusinessUnitId,
                                                        p_TransDate, p_TotalProportion, p_ApprovalStatus, p_Comments,
                                                        p_ApproverComments, p_TotalContiProportion, p_DisConfirmFlag,
                                                        p_DisUnderstandFlag, p_DisFormLineId, p_DisFormId,
                                                        p_RelationshipType, p_FullName, p_Proportion,
                                                        p_PrimaryContactFlag, p_SecondaryContactFlag, p_MobileNumber,
                                                        p_MobileNumber1, p_EmailAddress, p_ResiAddress, p_DisBeneFlag,
                                                        p_DisEmerContactId, p_EmerDisFormId, p_EmerRelationshipType,
                                                        p_EmerFullName, p_EmerMobileNumber, p_EmerPrimaryContactFlag,
                                                        p_EmerSecondaryContactFlag, p_DisEmerFlag, p_DisContingentId,
                                                        p_ContiDisFormId, p_ContiRelationshipType, p_ContiFullName,
                                                        p_ContiProportion, p_ContiMobileNumber, p_ContiMobileNumber1,
                                                        p_ContiEmailAddress, p_ContiResiAddress);

                System.err.println("xmlData =>" + xmlData);

                a = ApprovalProcess.invokeWsdl(xmlData, disFormWSDL, ApprovalPayload.DIS_FORM_METHOD);
                if (a[0] != null && a[0].equals("True")) {
                    OperationBinding binding = (OperationBinding) ADFUtils.findOperation("Commit").execute();
                    JSFUtils.addFacesInformationMessage("API Form Submitted Successfully");
                    value = true;
                } else {
                    JSFUtils.addFacesInformationMessage("Error");
                    disFormHdrRowImpl.setApprovalStatus("DRAFT");
                    //value = false;

                }

            }
        } else {
            JSFUtils.addFacesErrorMessage("Atleast One Emergency Primary Contact should be selected.");
            // value = true;
        }

        if (value) {
            disFormHdrVO.applyViewCriteria(null);
            disFormHdrVO.executeQuery();
            return "back";
        } else {
            return null;

        }

        //        else {
        //            JSFUtils.addFacesErrorMessage("Atleast one Primary Contact should be selected. Please Select.");
        //        }
    }

    public void onClickEmerPrimaryFlag(ValueChangeEvent valueChangeEvent) {
        valueChangeEvent.getComponent().processUpdates(FacesContext.getCurrentInstance());
        ViewObject customerVo = ADFUtils.findIterator("XXSSHR_DIS_EMERGENCY_DETAILS_VOIterator").getViewObject();
        RowSetIterator dtlsRS = customerVo.createRowSetIterator(null);
        int currIndex = customerVo.getCurrentRowIndex();
        int i = 0;
        while (dtlsRS.hasNext()) {
            Row r = dtlsRS.next();
            System.err.println("Emer PrimaryFlag--" + r.getAttribute("EmerPrimaryContactFlag"));
            if (i == currIndex) {
                System.err.println("Emer Current row" + currIndex);
                i++;
                continue;
            }
            System.err.println("set false");
            r.setAttribute("EmerPrimaryContactFlag", "N");
            i++;
        }
        System.out.println("EmerRelationshipType EmerRelationshipType--------------- " +
                           customerVo.getCurrentRow().getAttribute("EmerRelationshipType"));
        if (customerVo.getCurrentRow()
                      .getAttribute("EmerPrimaryContactFlag")
                      .equals("Y")) {
            customerVo.getCurrentRow().setAttribute("EmerSecondaryContactFlag", "N");
        }
        AdfFacesContext.getCurrentInstance().addPartialTarget(emergencytab);

    }


    public void onClickEmerSecondaryFlag(ValueChangeEvent valueChangeEvent) {
        valueChangeEvent.getComponent().processUpdates(FacesContext.getCurrentInstance());
        ViewObject emerDetailsVO = ADFUtils.findIterator("XXSSHR_DIS_EMERGENCY_DETAILS_VOIterator").getViewObject();
        if (emerDetailsVO.getCurrentRow() != null) {
            System.out.println("Emer Relation ship --- " +
                               emerDetailsVO.getCurrentRow().getAttribute("EmerRelationshipType"));
            String primaryFlag = emerDetailsVO.getCurrentRow()
                                              .getAttribute("EmerPrimaryContactFlag")
                                              .toString();
            System.out.println("Current primaryFlag--------------- " + primaryFlag);
            if (primaryFlag.equalsIgnoreCase("Y")) {
                emerDetailsVO.getCurrentRow().setAttribute("EmerPrimaryContactFlag", "N");
            }
        }

        AdfFacesContext.getCurrentInstance().addPartialTarget(emergencytab);
    }

    public void setEmerPrimaryContactFlag(RichSelectBooleanCheckbox emerPrimaryContactFlag) {
        this.emerPrimaryContactFlag = emerPrimaryContactFlag;
    }

    public RichSelectBooleanCheckbox getEmerPrimaryContactFlag() {
        return emerPrimaryContactFlag;
    }

    public void setEmerSecondaryContactFlag(RichSelectBooleanCheckbox emerSecondaryContactFlag) {
        this.emerSecondaryContactFlag = emerSecondaryContactFlag;
    }

    public RichSelectBooleanCheckbox getEmerSecondaryContactFlag() {
        return emerSecondaryContactFlag;
    }

    public void setEmergencytab(RichTable emergencytab) {
        this.emergencytab = emergencytab;
    }

    public RichTable getEmergencytab() {
        return emergencytab;
    }

    public void setContingentTable(RichTable contingentTable) {
        this.contingentTable = contingentTable;
    }

    public RichTable getContingentTable() {
        return contingentTable;
    }

    public void setContiPrimaryContactFlag(RichSelectBooleanCheckbox contiPrimaryContactFlag) {
        this.contiPrimaryContactFlag = contiPrimaryContactFlag;
    }

    public RichSelectBooleanCheckbox getContiPrimaryContactFlag() {
        return contiPrimaryContactFlag;
    }

    public void setContiSecondaryContactFlag(RichSelectBooleanCheckbox contiSecondaryContactFlag) {
        this.contiSecondaryContactFlag = contiSecondaryContactFlag;
    }

    public RichSelectBooleanCheckbox getContiSecondaryContactFlag() {
        return contiSecondaryContactFlag;
    }

    public void onClickContiPrimaryFlag(ValueChangeEvent valueChangeEvent) {
        valueChangeEvent.getComponent().processUpdates(FacesContext.getCurrentInstance());
        ViewObject contingentVO = ADFUtils.findIterator("XxsshrDisContingentLinesVOIterator").getViewObject();
        RowSetIterator dtlsRS = contingentVO.createRowSetIterator(null);
        int currIndex = contingentVO.getCurrentRowIndex();
        int i = 0;
        while (dtlsRS.hasNext()) {
            Row r = dtlsRS.next();
            System.err.println("ContiPrimaryContactFlag--" + r.getAttribute("ContiPrimaryContactFlag"));
            if (i == currIndex) {
                System.err.println("ContiPrimaryContactFlag Current row");
                i++;
                continue;
            }
            System.err.println("set false");
            r.setAttribute("ContiPrimaryContactFlag", "N");
            i++;
        }
        AdfFacesContext.getCurrentInstance().addPartialTarget(contingentTable);
    }
}
