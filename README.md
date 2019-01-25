add example

    getToken: function () {

        var checkToken = localStorage.getItem("notifyToken");
        if (!checkToken)
            window.FirebasePlugin.getToken(function (token) {
                // save this server-side and use it to push notifications to this device
                console.log(token);
                localStorage.setItem("notifyToken", token);
            }, function (error) {
                console.error(error);
            });
        else
            console.log(checkToken);
    },
    refreshToken: function () {
        window.FirebasePlugin.onTokenRefresh(function (token) {
            // save this server-side and use it to push notifications to this device
            console.log(token);
        }, function (error) {
            console.error(error);
        });
    },
    getNotification: function () {
        window.FirebasePlugin.onNotificationOpen(function (notification) {
            if (notification.tap) {
                // alert("APP outside")
                var url = notification.url;
                try {
                    if (!!url)
                        window.location.replace(url);
                    else
                        window.location.replace("index.html");
                } catch (error) {
                    console.log(error);
                }
            }
            else {
                alert("App inside")
            }
            console.log(notification);
        }, function (error) {
            console.error(error);
        });
    }
