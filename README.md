# Reusable AngularJs BootStrap Modal
**Project Description:** An AngualarJs Modal component based on Bottstrap Modal that is resuable              
**Author:** Eric Chen                            
**Blog:** http://www.hitechchimp.com
# Installation
##### 1. Install BootStrap and Angular-xeditable in your project: 
This modal us Angular-xeditable, so the fisrt step is to include it in your project
https://vitalets.github.io/angular-xeditable/
##### 2. Include the modal componet in your project,
Example: https://github.com/cxywind/WsCRM/blob/master/WsCRM/index.html
##### 3.Add dependency of the Modal
Example: https://github.com/cxywind/WsCRM/blob/master/WsCRM/App/wscrm.module.js

# How to use it?
#### 1. Code in template:
```
<c-modal></c-modal> 
```
Make sure the code is under the controll of the view's conresponding controller

#### 2. Code in conresponding controller

Example: https://github.com/cxywind/WsCRM/blob/master/WsCRM/App/orders/order.html

Following code is required by xeditable
```
 .run(function(editableOptions) {
      editableOptions.theme = 'bs3'; // xeditable
})
```

Add dependency on utils.
```
controller: function OrderListController($scope, $rootScope, utils) {
```

 toModalObject(): prepare modal form data                        
 title: title for input                                 
 variableName: dababase filed name                      
 type: input type  
 hide: hide this line
 value: setting the initial value if you edit a entity by modal                        
 validation: minLen:2,maxLen:20,required: true                       
 regulation expression vaidation, regExpVaid: { text: 'Email format is not correct', reg: /^\s*\w*\s*$/ }, see the example

```
 $scope.toModalObject = function (table) {
            var orderToModal = [
                    { title: 'Domain', hide: true, variableName: 'Domain', value: (order ? order.Domain : ''), type: 'text', validation: { minLen: 2, maxlen:20 errorText: '* required' } },
                    { title: 'Email', variableName: 'Email', value: (order ? order.Email : ''), type: 'email', validation: { required: true, errorText: '* please input your email' }, regExpVaid: { text: 'Email?????', reg: /^\s*\w*\s*$/ } },
                    { title: 'Phone', variableName: 'Phone', value: (order ? order.Phone : ''), type: 'tel' },
                    { title: 'Order Status', variableName: 'OrderStatus', value: (order ? order.OrderStatus : 0), type: 'select', selectEnum: $scope.orderStatus },
                    { title: 'Order Date', variableName: 'OrderDate', value: (order ? order.OrderDate : new Date()), type: 'date' },
                    { title: 'Marketing Way', variableName: 'MarketingWay', value: (order ? order.MarketingWay : 0), type: 'select', selectEnum: $scope.marketingWay },
                    { title: 'Product Name', variableName: 'ProductName', value: (order ? order.ProductName : ''), type: 'text' },
                    { title: 'Description', variableName: 'Description', value: (order ? order.Description : ''), type: 'textarea' }
            ];

            return orderToModal;
        };
```
showModal(): Called by when you click the button to show and render the modal. The modalOption is used to formulate the URL that $http.post() method called to. the Whole value of the Modal form will be send to Web API as an object.

Route:  domain/controller/action/idValue

```
        $scope.showModal = function () {
            var modalOption = {
                modalTitle: 'Get passowrd',  // Modal tilte
                controller: 'account', //Contorll name 
                action: 'getPassword', //Action Name (Post)
                idVariable: 'UserId', // ID of a table
		idValue: '12', // nuallable， the id of the entity, when create new, keep empty
                httpPostConfig: {
                      headers: {
                          'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8;'
                      }
                  }
$scope.showModal = function () {
            var modalOption = {
                modalTitle: 'Get passowrd',  // Modal tilte
                controller: 'account', //Contorll name 
                action: 'getPassword', //Action Name (Post)
                idVariable: 'UserId', // ID of a table
        idValue: '12', // nuallable， the id of the entity, when create new, keep empty
                httpPostConfig: {
                      headers: {
                          'Content-Type': 'application/x-www-form-urlencoded;charset=utf-8;'
                      }
                  }
            };
            };

            $scope.$broadcast('showModelEvent', [$scope.toModalObject(), modalOption]);
        };

```
`Do something here when click the save button on the modal, when the save action success or failed. 
```
       $scope.$on('modelDone', function (event, data) {
              if (data[1]) {
                  console.log(data[0]);  // data[0] populate the response from server
                  console.log('Success');
              } else {
                  console.log('error');
              }
          });
`
```
####Don't forget this:
add showModal() to ng-click 

———————————————————————Advance————————————————————————

#### 1. Render select 

 ```
 { title: 'Order Status', variableName: 'OrderStatus', value: (order ? order.OrderStatus : 0), type: 'select', selectEnum: $scope.orderStatus }
 ```
 ```
  $scope.orderStatus = [
              { value: 0, text: 'Deposit paid' },
              { value: 1, text: 'Paid' },
              { value: 2, text: 'Canceled' },
              { value: 3, text: 'Refunded' },
              { value: 4, text: 'Expire' }
          ];
 ```

#### 2. Using the modal without post data to back-end

First, remove controller, action and httpPostConfig in the modalOption objcect

```
$scope.showModal = function () {
            var modalOption = {
                modalTitle: 'Get passowrd',  // Modal tilte
                idVariable: 'UserId', // ID of a table
                idValue: '12', // nuallable， the id of the entity, when create new, keep empty
            };

```
 
Then, using the data here
```
$scope.$on('modelDone', function (event, data) {
         console.log(data);    
          });
```


