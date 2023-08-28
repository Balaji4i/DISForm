package view;

import com.view.utils.ADFUtils;

import javax.faces.event.ActionEvent;

import oracle.adf.share.ADFContext;

import oracle.jbo.Row;
import oracle.jbo.RowSetIterator;
import oracle.jbo.ViewCriteria;
import oracle.jbo.ViewCriteriaRow;
import oracle.jbo.ViewObject;

public class SearchDISForm {
    private String disableDeleteIcons;

    public SearchDISForm() {
    }

    public void onClickEdit(ActionEvent actionEvent) {
        Object obj = ADFContext.getCurrent()
                               .getPageFlowScope()
                               .get("headerId");
        System.err.println("Object Name" + obj);
        ViewObject HdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        ViewCriteria hdrVC = HdrVO.createViewCriteria();
        ViewCriteriaRow hdrVcr = hdrVC.createViewCriteriaRow();
        hdrVcr.setAttribute("DisFormId", obj);
        hdrVC.addRow(hdrVcr);
        HdrVO.applyViewCriteria(hdrVC);
        HdrVO.executeQuery();
    }

    public void onClickDelete(ActionEvent actionEvent) {
        ADFUtils.findOperation("Delete").execute();
        ADFUtils.findOperation("Commit").execute();
    }

    public void setDisableDeleteIcons(String disableDeleteIcons) {
        this.disableDeleteIcons = disableDeleteIcons;
    }

    public String getDisableDeleteIcons() {
        ViewObject HdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        RowSetIterator rs = HdrVO.createRowSetIterator(null);
        while (rs.hasNext()) {
            Row r = rs.next();
            System.out.println("Count ----- " + HdrVO.getEstimatedRowCount());
            System.out.println("ApprovalStatus ----- " + r.getAttribute("ApprovalStatus"));
            if (r.getAttribute("ApprovalStatus").equals("DRAFT")) {
                System.out.println("Inside if loop----------");
                setDisableDeleteIcons("false");
            }
        }
        rs.closeRowSetIterator();
        return disableDeleteIcons;
    }

    public String getDisableAddIcons() {
        ViewObject HdrVO = ADFUtils.findIterator("XXSSHR_DIS_FORM_Hdr_VOIterator").getViewObject();
        RowSetIterator rs = HdrVO.createRowSetIterator(null);
        int i = 0;
        while (rs.hasNext()) {
            Row r = rs.next();
            System.out.println("Count in add method ----- " + HdrVO.getEstimatedRowCount());
            System.out.println("ApprovalStatus in add method ----- " + r.getAttribute("ApprovalStatus"));
            if (r.getAttribute("ApprovalStatus").equals("SUBMITTED") && HdrVO.getEstimatedRowCount() > 0) {
                System.out.println("Inside if loop----------");
                i++;
                continue;

            }
        }
        if (i > 0) {
            System.out.println("Into I If loop ------");
            setDisableDeleteIcons("true");
        }
        rs.closeRowSetIterator();
        return disableDeleteIcons;
    }

}
