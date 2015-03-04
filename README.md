Yii2 компонент платежной системы Perfect Money
----------------------------------------------

## Особенности

**Компонент обеспечивает простой и расширяемый функционал для работы с платежной системой [Perfect Money](http://perfectmoney.is)**


## Установка

Предпочтительный способ установки этого виджета через [composer](http://getcomposer.org/download/).

Запустите в консоле

```
php composer.phar require nepster-web/yii2-component-perfectmoney: dev-master
```

или добавьте

```
"nepster-web/yii2-component-perfectmoney": "dev-master"
```

в файл `composer.json` в секцию require.


## Настройка

Необходимо добавить настройку компонента в конфигурационный файл Вашего приложения:

```
'components' => [
    ...
    'pm' => [
        'class' => '\nepster\perfectmoney\Api',
        'accountId' => '0000000',
        'accountPassword' => '*******',
        'walletNumber' => 'U0000000',
        'merchantName' => 'Название компании',
        'alternateSecret' => 'Секретная фраза',
        'resultUrl' => ['/merchant/perfect-money/result'],
        'successUrl' => ['/merchant/perfect-money/success'],
        'failureUrl' => ['/merchant/perfect-money/failure'],
    ];
]
```

После успешной установки Вам будет доступен виджет с платежной формой, задача которого сделать автоматический редирект на сайт платежной системы:

```
return \common\widgets\perfectmoney\RenderForm::widget([
   'api' => Yii::$app->pm,
   'invoiceId' => $invoiceId,
   'amount' => $amount,
   'description' => 'Пополнение внутреннего счета',
   'autoRedirect' => true,
]);
```

**Обратите внимание**
Редирект реализован с помощью JavaScript, поэтому если он будет выключен, то пользователю необходимо подтвердить переход нажав на кнопку.

Виджет можно реализовать подходящим для Вас способом.