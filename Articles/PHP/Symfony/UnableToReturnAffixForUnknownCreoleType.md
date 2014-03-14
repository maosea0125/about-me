When start "symfony propel-build-model" get an error: Unable to return 'affix' for unknown CreoleType:  
----------

__Problem__  
When start "symfony propel-build-model" get an error:  

    [propel-om] + payment_paypal
    [propel-om] -> BasePaymentPaypalPeer [builder: SfPeerBuilder]
    [propel-om] -> BasePaymentPaypal [builder: SfObjectBuilder]
    [phingcall] Unable to return 'affix' for unknown CreoleType:


__Reason__  
That is not a problem of PHP 5.3 + SL, even though it happend after the update.  
It's rather a Creole problem.  

Check CreoleTypes.php (usually @ symfony/lib/vendor/creole/CreoleTypes.php)  

There the two constants TEXT and LONGVARCHAR are both defined as (int) 17.  

At lines 90-116 the creoleMapType array is populated, with the integer-constants as keys.  
Both self::TEXT and self::LONGVARCHAR will be assigned a value, their corresponding String values.  

But as they are both 17 only one of them can survive ...  
Apparently php 5.2.x used to overwrite the early 17 (TEXT) with the later (LONGVARCHAR) and apparently that behaviour has changed with 5.3 so that   "LONGVARCHAR" is no longer known as a creoleMapType.  


__How to fix__  
In lib/vendor/creole/CreoleTypes.php Line 39 changed  
    const TEXT = 17;  
to  
    const TEXT = 30; //php 5.3.0 fix, using an unused int