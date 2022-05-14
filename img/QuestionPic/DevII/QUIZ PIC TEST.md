# QUIZ PIC TEST



## 48

![48](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-48.jpg)

```java
A developer has a Batch Apex process, Batch_Account_Sales, that updates the sales amount for 10,000 Accounts on a nightly basis. 
The Batch Apex works as designed in the sandbox. However, the developer cannot get code coverage on the Batch Apex class.The test class is below:

@isTest
private class Batch_Account_Update_Test {
    @isTest
    static void UnitTest() {
        Account a = new Account(Name='test', Type='Customer', Sales_Amount__c=0);
        insert a;
        Batch_Account_Sales bas = new Batch_Account_Sales();
        ID jobid = Database.executeBatch(bas);
    }
}

What is causing the code coverage problem?
```





## 50

![50](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-50.jpg)

```java
trigger ContactTrigger on Contact (before insert, before update) 
{
	Map<Id, Account> accountMap = new Map<Id, Account>();
	for(Contact c : Trigger.new)
	{
		Account a = [SELECT Id, Name, BillingCountry FROM Account WHERE Id := c.AccountId];
		accountMap.put(a.Id, a);
	 }

	//Do stuff with accountMap
	for(Contact c : Trigger.new)
	{
		  Account a = accountMap.get(c.AccountId);
		  if(a != null) 
		  {
				 c.BillingCountry = a.BillingCountry;
		   }
	  }
	
	  update Trigger.new;

}
Refer to the code segment above

When following best practices for writing Apex triggers, which two lines are wrong or cause for concern?Choose 2 answers
```

## 52

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-52.jpg)

```java
Refer to the code snippet below:
01  public void createChildRecord(String externalIdenifier) {
02      Account parentAccount;
03
04      Contact newContact = new contact();
05      newContact.Account = parentAccount;
06
07       insert(newContact);
08  }
As part of an integration development effort, a developer is tasked to create an Apex method that solely relies on the use of foreign identifiers in order to relate new contact records to existing Accounts in Salesforce. The account object contains a field marked as an external ID, the API Name of this field is Legacy_Id__c.

What is the most efficient way to instantiate the parentAccount variable on line 02 to ensure the newly created contact is properly related to the Account?
```

## 53

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-53.jpg)

```java
trigger AssignOwnerByRegion on Account(before insert, before update){   
    List<Account> accountList = new List<Account>();   
    for(Account anAccount : trigger.new )   {      
        Region__c theRegion = [SELECT Id, Name, Region_Manager__c FROM Region__c 
                               WHERE Name= :anAccount.Region_Name__c];
        anAccount.OwnerId = theRegion.Region_Manager__c;  
        accountList.add(anAccount);   
    }   
    update accountList;
}
Consider the above trigger intended to assign the Account to the manager of the Account's region.Which two changes should a developer make in this trigger to adhere to best practices? Choose 2 answers
```

## 55

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-55.jpg)

```java
for ( Contact c : [SELECT Id, LastName FROM Contact WHERE CreatedDate = TODAY] )
{
    Account a = [SELECT Id, Name FROM Account WHERE CreatedDate = TODAY LIMIT 5];
    c.AccountId = a.Id;
    update c;
}
```



## 56

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-56.jpg)

```java
A developer created an Apex class that makes an outbound RESTful callout. The following class was created to send a fake response in Apex test methods.
@isTest
public class TestHttpCalloutMock implementsHttpCalloutMock {          
    public HTTPResponse respond (HTTPRequest request) {                  
        HttpResponse response = new HttpResponse( ) ;
        response.setHeader ('Content-Type ' ,'application/json'); 
        response.setBody(' {"colors": ["red", "blue", "yellow", "green", "pink"]}');  
        response.setStatusCode (200);
        return response;
}}
Which method can be called to return this fake response in the test methods?
```

## 57

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-57.jpg)

```JAVA
public class myServerSideController {       
    @AuraEnabled       
    public static MyDataWrapper getSomeData( String theType ) {              
        Some_Object__c someObj = [SELECT ID, Name FROM Some_Object__c 
                                  WHERE Type__c= :theType LIMIT 1];  
        
        Another_object__c anotherObj = [SELECT ID, Option__c FROM Another_Object__c 
                                        WHERE Some_Object__c = :someObj.Name LIMIT 1];   
        
        MyDataWrapper theData = new MyDataWrapper( );            
        theData.Name = someObj.Name;            
        theData.Option = anotherObj.Option__c;           
        return theData;    
    }    
    
    public class MyDataWrapper {
        public String Name { get; set; }
        public String Option { get; set; } 
        public MyDataWrapper () {}    
    }
}
Consider the controller code above that is called from a Lightning component and returns data wrapped in a class.The developer verified that the queries return a single record each and there is error handling in the Lightning component, but the component is not geting anything back when calling the controller getSomeData( ).What is wrong?
```

## 58

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-58.jpg)

```java
Refer to the code snippet below:
public static void updateCreditMemo(String customerId, Decimal newAmount) {     
    List<Credit_Memo__c> toUpdate = new List<Credit_Memo__c>( ) ;     
    for (Credit_Memo__c creditMemo : [Select Id, Name, Amount__c FROM Credit_Memo__c 
                                      WHERE Customer_Id__c = : customerId LIMIT 50]) {           
         creditMemo.Amount__c = newAmount;           
         toUpdate.add(creditMemo) ;      
    }
    Database.update(toUpdate, false);
}
A custom object called Credit_Memo__c exists in a Salesforce environment. As part of a new feature development that retrieves and manipulates this type of record, the developer needs to ensure race conditions are prevented when a set of records are modified within an Apex transaction.In the preceding Apex code, how can the developer alter the query statement to use SOQL features to prevent race conditions within a transaction?
```



## 59

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-59.jpg)

```JAVA
public class LeadController {
    
    public static List<Lead> getFetchLeadList (String searchTerm, Decimal aRevenue) {
        
        String safeTerm = '%'+searchTerm. escapeSingleQuote( )+'%'
            return [
                SELECT Name, Company, AnnualRevenue
                FROM Lead
                WHERE AnnualRevenue >= :aRevenue
                AND Company LIKE : safeTerm;
                LIMIT 20
            ];
    }
}
```

## 60

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-60.jpg)

```JAVA
A company has code to update a Request and Request Lines and make a callout to their external ERP system's REST endpoint with the updated records.
public void updateAndMakeCallout(Map<Id, Request__c> reqs, Map<Id, Request_Line__c> reqLines) {
        Savepoint sp = Database.setSavepoint( );
        try {
             insert reqs.values( );
             insert reqLines.values( );
             HttpResponse response = CalloutUtil.makeRestCallout(reqs.keySet(), reqLines.keySet());
        } catch (Exception e) {
             Database.rollback (sp) ;
             System.debug(e) ;
        }
}
The CalloutUtil.makeRestCallout fails with a 'You have uncommitted work pending. Please commit or rollback before calling out' error.
What should be done to address the problem?
```

## 61

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-61.jpg)

```java
  public class AttributeTypes
 {
  	private final String[] arrayItems;
 
  	@AuraEnabled
  	public List<String> getStringArray(){
   		String[] arrayItems = new String[]{ 'red', 'green', 'blue' };
   		return arrayItems;
 	}
 }
Consider the Apex controller above, that is called from a Lightning Aura Component. 
What is wrong with it?
```

## 62

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Process%20Automation%20and%20Logic%20PDII-62.jpg)

```java
Example 1:
AggregateResult[]  groupedResults = [SELECT Campaignid, AVG (Amount) FROM Opportunity GROUP BY CanpaignId];
for (AggregateResult ar : groupedResults )
{
     System.debug ( 'Campaign ID' +  ar.get ('CampaignId; ) ) ;
     System.debug ( 'Average amount ' + ar.get('expr0' ) ) ;
}

Example 2 :
AggregateResult[]  groupedResults  = [SELECT CampaignId, AVG (Amount) theAverage FROM Opportunity GROUP BY CampaignId] ;
for (AggregateResult ar : groupedResults) 
{
     System.debug('Campaign ID' + ar.get('CampaignId') ) ;
     System.debug ( 'Average amount ' + ar.get('theAverage ' ) ) ;
}

Example 3:
AggregateResult[]  groupedResults = [SELECT CampaignId, AVG (Amount) FROM Opportunity GROUP BY CampaignId];
for (AggregateResult ar : groupedResults)
{
     System.debug ( 'Campaign ID' + ar.get (CampaignId') );
     System.debug ( 'Average amount'+ ar.get.AVG()) ;
}

Example 4:
AggregateResult[]  groupedResults = [SELECT CampaignId, AVG (Amount) theAverage FROM Opportunity GROUP BY CampaignId];
for(AggregateResult ar : groupedResults )
{
     System.debug ( 'Campaign ID' + ar.get ('CampaignId' ));
     System.debug ( 'Average amount' + ar.theAverage) ;
}
Which two of the examples above have correct System debug statements?Choose 2 answers
```

## 82

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-82.jpg)

```javascript
import { LightningElement, api, wire } from 'lwc' ;
import { getRecord } from 'lightning/uiRecordApi' ;

export default class Record extends LightningElement {
    @api fields;
    @api recordId;
    record;
}
```

## 83

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-83.jpg)

```javascript
<lightning:button label="Save" onclick="{!c.handleSave}" />
({
       handleSave : function (component, event, helper) {
               helper.saveAndRedirect (component) ;
      }
})
```

## 85

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-85.jpg)

```html
<aura:component>
       <lightning:input type="Text" name="searchString" aura:id="search1" label="Search String"/>
       <br/>
       <lightning:button label="Search" onclick="{!c.performSearch)"/>
</aura:component>
```

## 86

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-86.jpg)

```JAVA
@isTest
static void testUpdateSuccess( ) {

    Account acct = new Account (Name = 'test') ;
    insert acct;

    // Add code here

    extension.inputValue = 'test';
    PageReference pageRef = extension.update( ); 
    System.assertNotEquals(null, pageRef) ;
}

```

## 92

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-92.jpg)

```java
Lightning Aura Component
<aura:component controller="SimpleServerSidecontroller">
	<aura:attribute name="firstName" type="String" default="world"/>
	<lightning:button label="Call server" onclick="{!c.echo}"/>
</aura:component>

Lightning Aura Controller
01 ({
02 	"echo" : function(cmp) {
03 		//create a one-time use instance of the serverEcho action
04 		//in the server-side controller
05 		var action = cmp.get("c.serverEcho");
06 		action.setParams({ firstName : cmp.get("v.firstName") });
07
08 		//Create a callback that is executed after
09 		//the server-side action returns
10 		action.setCallback(this, function(response) {
11  		var state = response.getState();
12  		if (state === "SUCCESS") {
13   			//Alert the user with the value returned
14   			// from the server
15   			alert("From server: " +response.getReturnValue()) ;
16
17   			//You would typically fire an event here to trigger
18   			// client-side notification that the server-side
19   			// action is complete
20  		}
21  		else if(state === "INCOMPLETE"){
22   			//do something
23  		}
24  		else if (state === "ERROR") {
25   			var errors = response.getError();
26   			if (errors) {
27    				if (errors [0] && errors[0].message) {
28     					console.log("Error message: " +
29      					errors[0] .message );
30    				}
31   			} else {
32    				console.log("Unknoown error");
33   			}
34  		}
35 		});
36
37 		//A client-side action could cause multiple events,
38 		//which could trigger other events and
39 		//other server-side action calls.
40 		// $A.enqueueAction adds the server-side action to the queue.
41 		$A.enqueueAction(action);
42 	}
43})

Apex Controller
01 public with sharing class SimpleServerSideController {
02
03    //Use @AuaEnabled to enable client- and server-side access to the method
04    @AuraEnabled
05    public static String serverEcho(JSONObject firstName) {
06   	  String firstNameStr = (String)JSON.deserialize(firstName, String,class);
07   	  return ('Hello from the server. ' + firstNameStr);
08    }
09 }
```

## 93

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-93.jpg)

```html
<lightning:layout multipleRows="true" >
    
    <lightning:layoutItem size="12"> {!v.account.Name} </lighting:layoutItem>
    <lightning:layoutItem size="12"> {!v.account.AccountNumber} </lighting:layoutItem>
    <lightning:layoutItem size="12"> {!v.account.Industry} </lighting:layoutItem>
    
</lightning:layout>
```



## 95

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/User%20Interface%20PDII-95.jpg)

```HTML
<apex:page standardController="Account">
         <apex:pageBlock title="Hello {! $User.FirstName}!">
            You are displaying contacts from the {!account.name} account. Click a contact's name to view his or her details.
         </apex:pageBlock>
		 
         <apex:pageBlock title="Contacts" >
            <apex:form>
              <apex:dataTable value=" {! account.Contacts}" var="contact" cellPadding="4" border="1">
                <apex:column>
                  <apex:commandLink rerender="detail">
                     {!contact.Name}
                     <apex:param name="cid" value="{!contact.id}"/>
                  </apex:commandLink>
               </apex:column>
             </apex:dataTable>
           </apex:form>
        </apex:pageBlock>

        <apex:outputPanel id="detail">
          <apex:detail subject="{!$CurrentPage.parameters.cid}" relatedList="faise" title="false"/>
        </apex:outputPanel>
</apex:page>
```

## 137

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Debug%20and%20Deployment%20Tools-137.jpg)

```java
Line 1: @isTest
Line 2: static void testMyTrigger()
Line 3: {
Line 4:      //Do a bunch of data setup
Line 5:      DataFactory.setupDataForMyTriggerTest();
Line 6:
Line 7:      List<Account> acctsBefore = [SELECT Is_Customer__c FROM Account WHERE Id IN :DataFactory.accounts];
Line 8:
Line 9:      //Utility to assert all accounts are not customers before the update
Line 10:    AssertUtil.assertNotCustomers(acctsBefore);
Line 11:
Line 12:     //Set accounts to be customers
Line 13:     for (Account a : DataFactory.accounts)
Line 14:     {
Line 15:          a.Is_Customer__c  = true; 
Line 16:     }
Line 17:
Line 18:     update DataFactory.accounts;
Line 19:
Line 20:     List<Account> acctsAfter = [SELECT Number_Of_Transfers__c FROM Account WHERE Id IN :DataFactory.accounts];
Line 21:
Line 22:     //Utility to assert Number_Of_Transfers__c is correct based on test data
Line 23:     AssertUtil.assertNumberOfTransfers(acctaAfter);
Line 24:  }
```

## 138

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Debug%20and%20Deployment%20Tools-138.jpg)

```JAVA
global with sharing class MyRemoter{
    
    public String accountName {get; set;}
    public static Account account {get; set;}
    public AccountRemoter() {}
    
    @RemoteAction
    global static Account getAccount(String accountName) {
        account = [SELECT Id, Name, NumberOfEmployees FROM Account WHERE Name = :accountName];
        return account;
    }
}
```

## 139

![](https://cdn.jsdelivr.net/gh/nxwzj0/image-bed@main/img/QuestionPic/DevII/Debug%20and%20Deployment%20Tools-139.jpg)

```java
@isTest
static void testAccountUpdate() {

      Account acct = new Account (Name = 'Test');
      acct.Integration_Updated_c = false;
      insert acct;

      CalloutUtil.sendAccountUpdate(acct.Id);
      Account acctAfter = [SELECT Id, Integration_Updated_c FROM Account WHERE Id = :acct.Id][0];
      System.assert(true, acctAfter.Integration_Updated_c );
}

```

