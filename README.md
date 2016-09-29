# Reusable AngularJs BootStrap Modal
**Project Description: ** An AngualarJs Modal component based on Bottstrap Modal that is resuable
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
1. Code in template:
```
<c-modal></c-modal> 
```
Make sure the code is under the controll of the view's conresponding controller

2. Code in conresponding controller

Example: https://github.com/cxywind/WsCRM/blob/master/WsCRM/App/orders/order.html

Following code is required by xeditable
```
 .run(function(editableOptions) {
      editableOptions.theme = 'bs3'; // xeditable
})
```

How to use:

Please look into the expample I put on page: https://localhost:44300/Account/ForgetPassword

```
 $scope.toModalObject = function (table) {
            var orderToModal = [
                    { title: 'Domain', variableName: 'Domain', value: (order ? order.Domain : ''), type: 'text', validation: { minLen: 2, maxlen:20 errorText: '* required' } },
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
        $scope.showModal = function () {
            var modalOption = {
                modalTitle: 'Get passowrd',  // Modal tilte
                controller: 'account', //Contorll name 
                action: 'getPassword', //Action Name (Post)
                idVariable: 'UserId', // ID of a table
		idvalue:'' //nuallable, Route domain/controller/action/idValue
            };

            $scope.$broadcast('showModelEvent', [$scope.toModalObject(), modalOption]);
        };

	
	//Do something here when click the save button on the modal, when save success or failed
        $scope.$on('modelDone', function (event, data) {
              if (data) {
                  console.log('Success');
              } else {
                  console.log('error');
              }
          });



3. add showModal() to ng-click 

—————————————————————————advance—————————————————————————————————————————————
1. add dropdown input
 $scope.showModal = function () {
            var modalOption = {
                modalTitle: 'Forget your password?',
                controller: 'account',
                action: 'getPassword',
                idVariable: 'UserId',
                idValue: '12'
            };

            $scope.$broadcast('showModelEvent', [$scope.toModalObject(), modalOption]);
};

add the following object to orderToModal : { title: 'Marketing Way', variableName: 'MarketingWay', value: (order ? order.MarketingWay : 0), type: 'select', selectEnum: $scope.marketingWay },




 

Add dependency on utils.
```
controller: function OrderListController($scope, $rootScope, utils) {
```

