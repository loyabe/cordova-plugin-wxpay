# cordova-plugin-wxpay
使用2015-03-09发布的WeX5版本，下面的参数是起步公司申请的微信支付账号

1、修改微信插件的支付参数
修改/Native/plugins/com.justep.cordova.plugin.weixin/plugin.xml文件

            <preference name="weixinappid" value="wx832f85feb2e76b14" />
                    <preference name="partner_id" value="1230177801" />
                    <preference name="partner_key" value="be9aded460e78703b889f18e2915ea6b" />
                    <preference name="app_secret" value="43cab6b2766381683f6cb1b4ee6db27a" />
                    <preference name="app_key" value="8e5UlAqM5tJr7gVnbiPJbO6ZXFgwHAQ6mHaohjvTpbuTvnsZWuNlGsooC8Rp8owsSS5TcnAW1caNamUGL8w8GuESCCftDzNarmmRKqGRhFAdqomDjRSgAL2HezQ1iCZz" />

2、调用支付方法

        var weixin = navigator.weixin;
        weixin.getAccessToken(function(accessToken){
                console.log('accessToken:' + accessToken);
                
                weixin.generatePrepayId(
                                {"body":"x5",
                                        "accessToken":accessToken,
                                        "feeType":"1",
                                        "notifyUrl":"http://www.justep.com",
                                        "totalFee":"1",
                                        "traceId":'123456',
                                        "tradeNo":"123456789"},
                                        function(prepayId){
                                                console.log('prepayId:' + prepayId);
                                                weixin.sendPayReq(prepayId,function(){
                                                        console.log('prepayId success');
                                                        alert("success");
                                                },function(message){
                                                        alert("sendPayReq:"+ message);
                                                });
                                        },function(message){
                                                alert("getPrepayId:" + message);
                                        }
                );
        },function(message){
                alert("getToken:" + message);
        });

3、新建本地app
应用包名必须输入com.justep.x5.v3，选择源代码模式，使用打包服务器打包，生成app之后，可以调出支付窗口

4、注意如果修改了微信插件里面的支付参数，需要新建本地app，才能生效

5、如果使用自己的支付账号，可以通过下载安装http://open.weixin.qq.com/download/sdk/gen_signature.apk
来获取应用签名，并填写到网站
