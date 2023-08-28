package view;


import java.text.SimpleDateFormat;

import java.util.ArrayList;
import java.util.TimeZone;

public class ApprovalPayload {
    public ApprovalPayload() {
        super();
    }
   
    
    //bUSINESS
     /***Cloud purpose un comment these section while deploying to TEST cloud **/ 
     public static final String BUDDY_CARE_WSDL = "http://oaosoatst-wls-1.sub08071802371.oandopaasvcn.oraclevcn.com:9073/soa-infra/services/default/BuddyCareApproval/bpelprocess1_client_ep?WSDL";
    //public static final String DUTY_ALLOWANCE_WSDL ="https://oaosoatest.oandoplc.com/soa-infra/services/default/ExtraDutyAllowanceApproval/allowanceapprovalprocess_client_ep?WSDL";
    public static final String BUDDY_CARE_METHOD = "process";
    
    /***Cloud purpose un comment these section while deploying to TEST cloud **/ 
    public static final String DUTY_ALLOWANCE_WSDL = "http://oaosoatst-wls-1.sub08071802371.oandopaasvcn.oraclevcn.com:9073/soa-infra/services/default/ExtraDutyAllowanceApproval/allowanceapprovalprocess_client_ep?WSDL";
    //public static final String DUTY_ALLOWANCE_WSDL ="https://oaosoatest.oandoplc.com/soa-infra/services/default/ExtraDutyAllowanceApproval/allowanceapprovalprocess_client_ep?WSDL";
    public static final String DUTY_ALLOWANCE_METHOD = "process";
    
    
    /***Cloud purpose un comment these section while deploying to TEST cloud **/ 
    public static final String DIS_FORM_WSDL = "http://oaosoatst-wls-1.sub08071802371.oandopaasvcn.oraclevcn.com:9073/soa-infra/services/default/DISForm/disbpelprocess_client_ep?WSDL";
    
    public static final String DIS_FORM_METHOD = "process";
   
    /***Cloud purpose un comment these section while deploying to PROD cloud **/    
  // public static final String DIS_FORM_WSDL ="http://oaosoaprd-wls-1.sub08071802370.oandopaasvcn.oraclevcn.com:9073/soa-infra/services/default/DISForm/disbpelprocess_client_ep?WSDL";


    public static String businessTypeXMLData(String p_EmployeeName, String p_EmployeeNumber, String p_Email,
                                             String p_BusinessGroup, String p_Cadre, String p_DisFormID,
                                             String p_DisFormNo, String p_PersonId, String p_BusinessUnitId,
                                             String p_TransDate, String p_TotalProportion, String p_ApprovalStatus,
                                             String p_ApproverComments,String p_Comments, String p_TotalContiProportion,
                                             String p_DisConfirmFlag, String p_DisUnderstandFlag,
                                             ArrayList p_DisFormLineId,
                                             ArrayList p_DisFormId, ArrayList p_RelationshipType, ArrayList p_FullName,
                                             ArrayList p_Proportion, ArrayList p_PrimaryContactFlag,
                                             ArrayList p_SecondaryContactFlag, ArrayList p_MobileNumber,
                                             ArrayList p_MobileNumber1, ArrayList p_EmailAddress, ArrayList p_ResiAddress,
                                             ArrayList p_DisBeneFlag,
                                             ArrayList p_DisEmerContactId, ArrayList p_EmerDisFormId,
                                             ArrayList p_EmerRelationshipType,
                                             ArrayList p_EmerFullName, ArrayList p_EmerMobileNumber,
                                             ArrayList p_EmerPrimaryContactFlag, ArrayList p_EmerSecondaryContactFlag,
                                             ArrayList p_DisEmerFlag,
                                             ArrayList p_DisContingentId, ArrayList p_ContiDisFormId,
                                             ArrayList p_ContiRelationshipType, ArrayList p_ContiFullName,
                                             ArrayList p_ContiProportion, ArrayList p_ContiMobileNumber,
                                             ArrayList p_ContiMobileNumber1, ArrayList p_ContiEmailAddress,
                                             ArrayList p_ContiResiAddress)
                                              {
        String[] info=payloadHeader();  
        String totalXml=null;
        String xmlData2="\n";
        String xmlData3="\n";
        String xmlData4="\n";
        System.err.println("Created time===>"+info[0]);
        System.err.println("User===========>"+info[1]);
        System.err.println("Password=======>"+info[2]);
        System.err.println("End time=======>"+info[3]);  
        String xmlData="<soapenv:Envelope xmlns:dis=\"http://xmlns.oracle.com/DISForm/DISForm/DISBPELProcess\" xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\">\n" + 
        "   <soapenv:Header/>\n" +  
        "   <soapenv:Body>\n" + 
               " <dis:process>\n" +                 
               "         <dis:EMPLOYEE_NUMBER>"+p_EmployeeNumber+"</dis:EMPLOYEE_NUMBER>\n" + 
               "         <dis:EMPLOYEE_NAME>"+p_EmployeeName+"</dis:EMPLOYEE_NAME>\n" +              
               "         <dis:EMAIL_ADDRESS>"+p_Email+"</dis:EMAIL_ADDRESS>\n" + 
               "         <dis:CADRE>"+p_Cadre+"</dis:CADRE>\n" + 
               "         <dis:BUSINESS_GROUP>"+p_BusinessGroup+"</dis:BUSINESS_GROUP>\n" +
               " <dis:HEADER>\n" +         
               "         <dis:DIS_FORM_ID>"+p_DisFormID+"</dis:DIS_FORM_ID>\n" + 
               "         <dis:DIS_FORM_NO>"+p_DisFormNo+"</dis:DIS_FORM_NO>\n" +              
               "         <dis:PERSON_ID>"+p_PersonId+"</dis:PERSON_ID>\n" + 
               "         <dis:BUSINESS_UNIT_ID>"+p_BusinessUnitId+"</dis:BUSINESS_UNIT_ID>\n" + 
               "         <dis:TRANSACTION_DATE>"+p_TransDate+"</dis:TRANSACTION_DATE>\n" +
               "         <dis:COMMENTS>"+p_Comments+"</dis:COMMENTS>\n" +
               "         <dis:TOTAL_PROPORTION>"+p_TotalProportion+"</dis:TOTAL_PROPORTION>\n" +
               "         <dis:APPROVAL_STATUS>"+p_ApprovalStatus+"</dis:APPROVAL_STATUS>\n" +
               "         <dis:APPROVER_COMMENTS>"+p_ApproverComments+"</dis:APPROVER_COMMENTS>\n" +
               "         <dis:DIS_CONFIRM_FLAG>"+p_DisConfirmFlag+"</dis:DIS_CONFIRM_FLAG>\n" +
               "         <dis:DIS_UNDERSTAND_FLAG>"+p_DisUnderstandFlag+"</dis:DIS_UNDERSTAND_FLAG>\n" +
               "         <dis:TOTAL_CONTI_PROPORTION>"+p_TotalContiProportion+"</dis:TOTAL_CONTI_PROPORTION>\n" +
               "         <!--1 or more repetitions:-->\n" ;            
                  for(int i=0;i < p_DisFormLineId.size() ;i++){ 
                    String tempXml=
                      "         <dis:BENEFICIARY>\n" + 
                              "         <dis:DIS_FORM_LINE_ID>"+p_DisFormLineId.get(i)+"</dis:DIS_FORM_LINE_ID>\n" + 
                              "         <dis:DIS_FORM_ID>"+p_DisFormId.get(i)+"</dis:DIS_FORM_ID>\n" + 
                              "         <dis:RELATIONSHIP_TYPE>"+p_RelationshipType.get(i)+"</dis:RELATIONSHIP_TYPE>\n" + 
                              "         <dis:FULL_NAME>"+p_FullName.get(i)+"</dis:FULL_NAME>\n" + 
                              "         <dis:PROPORTION>"+p_Proportion.get(i)+"</dis:PROPORTION>\n" + 
                              "         <dis:PRIMARY_CONTACT_FLAG>"+p_PrimaryContactFlag.get(i)+"</dis:PRIMARY_CONTACT_FLAG>\n" + 
                              "         <dis:SECONDARY_CONTACT_FLAG>"+p_SecondaryContactFlag.get(i)+"</dis:SECONDARY_CONTACT_FLAG>\n" +
                              "         <dis:MOBILE_NO>"+p_MobileNumber.get(i)+"</dis:MOBILE_NO>\n" +
                              "         <dis:MOBILE_NO1>"+p_MobileNumber1.get(i)+"</dis:MOBILE_NO1>\n" +
                              "         <dis:EMAIL_ADDRESS>"+p_EmailAddress.get(i)+"</dis:EMAIL_ADDRESS>\n" +
                              "         <dis:RESI_ADDRESS>"+p_ResiAddress.get(i)+"</dis:RESI_ADDRESS>\n" +
                              "         <dis:DIS_BENE_FLAG>"+p_DisBeneFlag.get(i)+"</dis:DIS_BENE_FLAG>\n" +
                      "         </dis:BENEFICIARY>\n" ;
                    xmlData2=xmlData2+"\n"+tempXml;
                          }
                  
        
                for(int j=0;j<p_DisEmerContactId.size() ;j++){ 
                    String tempXm3=
                      "         <dis:EMERGENCY>\n" + 
                              "         <dis:DIS_EMER_CONTACT_ID>"+p_DisEmerContactId.get(j)+"</dis:DIS_EMER_CONTACT_ID>\n" + 
                              "         <dis:DIS_FORM_ID>"+p_EmerDisFormId.get(j)+"</dis:DIS_FORM_ID>\n" + 
                              "         <dis:EMER_RELATIONSHIP_TYPE>"+p_EmerRelationshipType.get(j)+"</dis:EMER_RELATIONSHIP_TYPE>\n" + 
                              "         <dis:EMER_FULL_NAME>"+p_EmerFullName.get(j)+"</dis:EMER_FULL_NAME>\n" + 
                              "         <dis:EMER_MOBILE_NO>"+p_EmerMobileNumber.get(j)+"</dis:EMER_MOBILE_NO>\n" + 
                              "         <dis:EMER_PRIMARY_CONTACT_FLAG>"+p_EmerPrimaryContactFlag.get(j)+"</dis:EMER_PRIMARY_CONTACT_FLAG>\n" + 
                              "         <dis:EMER_SECONDARY_CONTACT_FLAG>"+p_EmerSecondaryContactFlag.get(j)+"</dis:EMER_SECONDARY_CONTACT_FLAG>\n" +
                              "         <dis:DIS_EMER_FLAG>"+p_DisEmerFlag.get(j)+"</dis:DIS_EMER_FLAG>\n" +
                      "         </dis:EMERGENCY>\n" ;
                    xmlData3=xmlData3+"\n"+tempXm3;
                          }
                
        for(int i=0;i < p_DisContingentId.size() ;i++){ 
          String tempXml1=
            "         <dis:CONTIBENEFICIARY>\n" + 
                    "         <dis:DIS_CONTINGENT_ID>"+p_DisContingentId.get(i)+"</dis:DIS_CONTINGENT_ID>\n" + 
                    "         <dis:CONTI_DIS_FORM_ID>"+p_ContiDisFormId.get(i)+"</dis:CONTI_DIS_FORM_ID>\n" + 
                    "         <dis:CONTI_RELATIONSHIP_TYPE>"+p_ContiRelationshipType.get(i)+"</dis:CONTI_RELATIONSHIP_TYPE>\n" + 
                    "         <dis:CONTI_FULL_NAME>"+p_ContiFullName.get(i)+"</dis:CONTI_FULL_NAME>\n" + 
                    "         <dis:CONTI_PROPORTION>"+p_ContiProportion.get(i)+"</dis:CONTI_PROPORTION>\n" +                    
                    "         <dis:CONTI_MOBILE_NO>"+p_ContiMobileNumber.get(i)+"</dis:CONTI_MOBILE_NO>\n" +
                    "         <dis:CONTI_MOBILE_NO1>"+p_ContiMobileNumber1.get(i)+"</dis:CONTI_MOBILE_NO1>\n" +
                    "         <dis:CONTI_EMAIL_ADDRESS>"+p_ContiEmailAddress.get(i)+"</dis:CONTI_EMAIL_ADDRESS>\n" +
                    "         <dis:CONTI_RESI_ADDRESS>"+p_ContiResiAddress.get(i)+"</dis:CONTI_RESI_ADDRESS>\n" +
            "         </dis:CONTIBENEFICIARY>\n" ;
          xmlData4=xmlData4+"\n"+tempXml1;
                }
                
        
               String xmlData5 =  " </dis:HEADER>\n" + "</dis:process>\n" + 
               "   </soapenv:Body>\n" + 
               "</soapenv:Envelope>";
               totalXml= xmlData+xmlData2 + "\n"+  xmlData3 + "\n" +  xmlData4 + "\n"+xmlData5;
               System.err.println("Totalxml"+totalXml);
               return totalXml;
       
    }


    public static String[] payloadHeader() {
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.000'Z'"); //Hours:Minutes:Seconds
        dateFormat.setTimeZone(TimeZone.getTimeZone("UTC"));
        java.util.Date date = new java.util.Date();
        long t = date.getTime();
        java.util.Date expDate;
        expDate = new java.util.Date(t + (10 * 600000000));
        String[] headerInfo = new String[4];
        headerInfo[0] = dateFormat.format(date);
        headerInfo[1] = "oaopdtst";
        headerInfo[2] = "O_0Pst#819";
        headerInfo[3] = dateFormat.format(expDate);
        return headerInfo;
    }
    
    public static String getUser(){        
        return null;
    }    
}