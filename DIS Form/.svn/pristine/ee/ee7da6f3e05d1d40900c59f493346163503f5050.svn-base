package view;

import com.view.utils.ADFUtils;

import com.view.utils.JSFUtils;

import java.math.BigDecimal;

import java.text.SimpleDateFormat;

import java.util.ArrayList;
import java.util.Date;

import javax.faces.event.ActionEvent;

import model.vo.DutyAllowance_VORowImpl;

import model.vo.XxsshrKnowBuddyCareVORowImpl;

import oracle.adf.model.OperationBinding;
import oracle.adf.model.binding.DCIteratorBinding;
import oracle.adf.share.ADFContext;

import oracle.jbo.Row;
import oracle.jbo.RowSetIterator;
import oracle.jbo.ViewCriteria;
import oracle.jbo.ViewCriteriaRow;
import oracle.jbo.ViewObject;

public class AddEditBuddyForm {
    public AddEditBuddyForm() {
        
    }
    
    public void onClickSave(ActionEvent actionEvent) {
        
        ViewObject vo = ADFUtils.findIterator("XxsshrKnowBuddyCareVOIterator").getViewObject();
        XxsshrKnowBuddyCareVORowImpl hdrRow = (XxsshrKnowBuddyCareVORowImpl) vo.getCurrentRow();       
        if (hdrRow != null) {
            hdrRow.setApprovalStatus("DRAFT");
        }
        ADFUtils.findOperation("Commit").execute();
        JSFUtils.addFacesInformationMessage("Know Buddy Care Form Saved Successfully");
    }


    public void onClickSubmit(ActionEvent actionEvent) {
        boolean result = false;
        if (!result) {
            DCIteratorBinding hdrIter = ADFUtils.findIterator("XxsshrKnowBuddyCareVOIterator");
            XxsshrKnowBuddyCareVORowImpl hdrRow = (XxsshrKnowBuddyCareVORowImpl) hdrIter.getCurrentRow();
            if (hdrRow != null) {
                hdrRow.setApprovalStatus("SUBMITTED FOR APPROVAL");
            }
            String xmlData = null;
            String[] a = null;
            String buddyCareWSDL = null;
            buddyCareWSDL = ApprovalPayload.BUDDY_CARE_WSDL;
            ViewObject HdrVo = ADFUtils.findIterator("XxsshrKnowBuddyCareVOIterator").getViewObject();
            
            String p_EmployeeName = HdrVo.getCurrentRow().getAttribute("Name_Trns") == null ? " " : HdrVo.getCurrentRow()
                                                                                                         .getAttribute("Name_Trns")
                                                                                                         .toString();
            String p_EmployeeNumber =
                HdrVo.getCurrentRow().getAttribute("Number_Trns") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                             .getAttribute("Number_Trns")
                                                                                                             .toString();
            String p_Email = HdrVo.getCurrentRow().getAttribute("Email_Trns") == null ? " " : HdrVo.getCurrentRow()
                                                                                                   .getAttribute("Email_Trns")
                                                                                                   .toString();
            String p_BusinessGroup = HdrVo.getCurrentRow().getAttribute("Group_Trns") == null ? " " : HdrVo.getCurrentRow()
                                                                                                           .getAttribute("Group_Trns")
                                                                                                           .toString();
            
            String p_Cadre =
                HdrVo.getCurrentRow().getAttribute("Trans_Cadre") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                              .getAttribute("Trans_Cadre")
                                                                                                              .toString();
            
            String p_AssignmentType =
                HdrVo.getCurrentRow().getAttribute("Trans_AssignmentType") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                              .getAttribute("Trans_AssignmentType")
                                                                                                              .toString();
            
            String p_BuddyCareNo =
                HdrVo.getCurrentRow().getAttribute("KnowBuddyCareNo") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                              .getAttribute("KnowBuddyCareNo")
                                                                                                              .toString();

            String p_TransDate = HdrVo.getCurrentRow().getAttribute("TransactionDate") == null ? " " : HdrVo.getCurrentRow()
                                                                                                            .getAttribute("TransactionDate")
                                                                                                            .toString();

            String p_DepartmentName =
                HdrVo.getCurrentRow().getAttribute("Trans_Value") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                                       .getAttribute("Trans_Value")
                                                                                                                       .toString();
            String p_PreviousApprover =
                HdrVo.getCurrentRow().getAttribute("PreviousApprover") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                                       .getAttribute("PreviousApprover")
                                                                                                                       .toString();
            
            String p_NextApprover =
                HdrVo.getCurrentRow().getAttribute("NextApprover") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                                       .getAttribute("NextApprover")
                                                                                                                       .toString();
            String p_ApprovalStatus =
                HdrVo.getCurrentRow().getAttribute("ApprovalStatus") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                                .getAttribute("ApprovalStatus")
                                                                                                                .toString();

            String p_Comments = HdrVo.getCurrentRow().getAttribute("Comments") == null ? " " : HdrVo.getCurrentRow()
                                                                                                    .getAttribute("Comments")
                                                                                                    .toString();

            String p_ApproverComments =
                HdrVo.getCurrentRow().getAttribute("ApproverComments") == null ? " " :
                HdrVo.getCurrentRow()
                                                                                                                    .getAttribute("ApproverComments")
                                                                                                                    .toString();
           
//            xmlData =
//                ApprovalPayload.businessTypeXMLData(p_EmployeeName, p_EmployeeNumber, p_Email, p_BusinessGroup,
//                                                    p_Cadre,p_AssignmentType, p_BuddyCareNo, p_TransDate,
//                                                    p_DepartmentName,p_PreviousApprover,p_NextApprover, p_ApprovalStatus,
//                                                    p_Comments, p_ApproverComments);
            System.err.println("xmlData =>" + xmlData);
            a = ApprovalProcess.invokeWsdl(xmlData, buddyCareWSDL, ApprovalPayload.BUDDY_CARE_METHOD);
            if (a[0] != null && a[0].equals("True")) {
                if (hdrRow != null) {
                    OperationBinding binding = (OperationBinding) ADFUtils.findOperation("Commit").execute();
                }
                JSFUtils.addFacesInformationMessage("Buddy Care Form Submitted Successfully");

            } else {
                JSFUtils.addFacesInformationMessage("Error");

            }

        }


    }
    
    public void onClickCancel(ActionEvent actionEvent) {
        ViewObject HdrVO = ADFUtils.findIterator("XxsshrKnowBuddyCareVOIterator").getViewObject();
        HdrVO.applyViewCriteria(null);
        HdrVO.executeQuery();
        ADFUtils.findOperation("Rollback").execute();
    }

    public void setOrgId() {
        Object obj = ADFContext.getCurrent()
                               .getSessionScope()
                               .get("personId");
        ViewObject empployeeROVO =
            ADFUtils.getApplicationModuleForDataControl("Oando_AMDataControl").findViewObject("Employee_View_ROVO");
        ViewCriteria viewCriteria = empployeeROVO.createViewCriteria();
        ViewCriteriaRow viewCriteriaRow = viewCriteria.createViewCriteriaRow();
        viewCriteriaRow.setAttribute("PersonId", obj);
        viewCriteria.addRow(viewCriteriaRow);
        empployeeROVO.applyViewCriteria(viewCriteria);
        empployeeROVO.executeQuery();
       // System.out.println("LineVo Query ----" + LineVo.getQuery());
        System.out.println("Person Id ----" + obj);

        if (empployeeROVO.getEstimatedRowCount() > 0) {
            Row row = empployeeROVO.first();
            row.getAttribute("BusinessUnitId");
            row.getAttribute("PersonNumber");
            row.getAttribute("FullName");
            row.getAttribute("EmailAddress");
            row.getAttribute("BusinessUnitName");
            row.getAttribute("DepartmentName");
            System.out.println(row.getAttribute("PersonNumber"));
            System.out.println(row.getAttribute("FullName"));
            System.out.println(row.getAttribute("EmailAddress"));
            System.out.println(row.getAttribute("BusinessUnitName"));
            System.out.println(row.getAttribute("DepartmentName"));
            Object orgObj = row.getAttribute("BusinessUnitId");
            ADFContext.getCurrent()
                      .getSessionScope()
                      .put("orgId", orgObj);


            System.out.println("111111111");
            ViewObject buddyCareVO =
                ADFUtils.getApplicationModuleForDataControl("Oando_AMDataControl").findViewObject("XxsshrKnowBuddyCareVO");
           // Row r = buddyCareVO.first();
            Row newRow = buddyCareVO.createRow();
            newRow.setAttribute("PersonId", obj);
            newRow.setAttribute("Name_Trns", row.getAttribute("FullName"));
            newRow.setAttribute("Number_Trns", row.getAttribute("PersonNumber"));
            newRow.setAttribute("Email_Trns", row.getAttribute("EmailAddress"));
            newRow.setAttribute("Group_Trns", row.getAttribute("BusinessUnitName"));
            newRow.setAttribute("BusinessUnitId", row.getAttribute("BusinessUnitId"));
            newRow.setAttribute("Trans_Value", row.getAttribute("DepartmentName"));
            buddyCareVO.insertRow(newRow);
        }

    }

}
