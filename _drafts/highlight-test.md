---
layout: post 
title: Test Highlighting
---

<!-- links -->
[setup-pygments]: https://truongtx.me/2012/12/28/jekyll-bootstrap-syntax-highlighting/

Test


Here's an example:

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```


[How to set up pygments and Highlight.js][setup-pygments]

Below is going to test Pygments Highlight

{% highlight java %}  
   private final BroadcastReceiver mReceiver = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            final String action = intent.getAction();

            Log.i(TAG,"BroadcastReceiver: action="+action);
            if(action.equals(Server_api.ACTION_GETUSER)) {
                user = intent.getParcelableExtra(Server_api.EXTRA_PARCEL);
                if(user==null) {
                    Log.e(TAG,"onReceive: ACTION_GETUSER, user null, should not enter here!");
                    return;
                    //server_api.newUser(user.getAccountType(), user.getAccount(), user.getFirst_name(), user.getLast_name());
                } else {
                    Log.i(TAG,"onReceive: ACTION_GETUSER, user found, get all coupons for user");
                    server_api.getAllCouponsForUser(user.getUser_id());
                    //goto_ActivityHome(userFromServer);
                }
            }

            else if(action.equals(Server_api.ACTION_GETALLCOUPONFORUSER)) {
                ArrayList<Coupon> coupons = intent.getParcelableArrayListExtra(Server_api.EXTRA_PARCEL_ARRAYLIST);
                Log.i(TAG,"ACTION_GETALLCOUPONFORUSER: coupons="+coupons);
                user.setCoupons(coupons);
                goto_ActivityHome(user);
            }

        }
    };
{% endhighlight %}


Below is going to test Highlight.js

	private final BroadcastReceiver mReceiver = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            final String action = intent.getAction();

            Log.i(TAG,"BroadcastReceiver: action="+action);
            if(action.equals(Server_api.ACTION_GETUSER)) {
                user = intent.getParcelableExtra(Server_api.EXTRA_PARCEL);
                if(user==null) {
                    Log.e(TAG,"onReceive: ACTION_GETUSER, user null, should not enter here!");
                    return;
                    //server_api.newUser(user.getAccountType(), user.getAccount(), user.getFirst_name(), user.getLast_name());
                } else {
                    Log.i(TAG,"onReceive: ACTION_GETUSER, user found, get all coupons for user");
                    server_api.getAllCouponsForUser(user.getUser_id());
                    //goto_ActivityHome(userFromServer);
                }
            }

            else if(action.equals(Server_api.ACTION_GETALLCOUPONFORUSER)) {
                ArrayList<Coupon> coupons = intent.getParcelableArrayListExtra(Server_api.EXTRA_PARCEL_ARRAYLIST);
                Log.i(TAG,"ACTION_GETALLCOUPONFORUSER: coupons="+coupons);
                user.setCoupons(coupons);
                goto_ActivityHome(user);
            }

        }
    };