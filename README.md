Country Code Picker Library
===========================

Country Code Picker (CCP) <img src="https://farm6.staticflickr.com/5726/30960801342_6e65c7ddd5_m.jpg" width="80">  is an android library which provides an easy way to search and select country phone code for the telephone number.

Introduction
------------
* CCP gives professional touch to your well designed form like login screen, sign up screen, edit profile screen. CCP removes confusion about how to add number and thus make view more understandable. Finally reduces mistakes in user input.
    * Phone number screen without CCP
          - <img src="https://raw.githubusercontent.com/hbb20/CountryCodePickerProject/master/app/src/main/res/drawable/img_c.png" width="300"> 
    * Above view can be transformed by using CCP
          - <img src="https://farm6.staticflickr.com/5625/30296514763_e3af239e2c_z.jpg" width="300">
    
    * Tapping on CCP will open a dialog to search and select country
          - <img src="https://farm6.staticflickr.com/5686/30982885732_294ee950d7_z.jpg" width="300">

How to add to your project
--------------

   1. Add this to your gradle file and sync

      ````groovy
        dependencies {
          compile 'com.hbb20:ccp:1.7.1'
        }
      ````

   2. Add ccp view to xml layout
   
      ````xml
        <com.countrypicker.CountryCodePicker
          android:id="@+id/ccp"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content" />
      ````

   3. Add ccp object in Activity / Fragment
   
      ````
        CountryCodePicker ccp;
      ````

   4. Bind ccp from layout
   
      ````
        ccp = (CountryCodePicker) findViewById(R.id.ccp);
      ````

   5. That's it. Run the project and see the results.

Features
--------
 - If you prefer experience along with only reads, an demo android app is available that demonstrates all the features of this library. Click below button to download from Playstore.
<br/><a href="https://goo.gl/zI2cY2"><img src="http://www.android.com/images/brand/get_it_on_play_logo_large.png"/></a>

 - If you just want to read them, here you go.
    ### 1. Default country###
    *  Default country is the country where most of your target audience belong.
    *  The default country can be set through xml layout and programmatically as well.
   
   - ####Through xml####
       **Using country code name**  
        - Add app:defaultNameCode="US" (replace "US" with your default country name code) to xml layout. Refer <a href="https://goo.gl/FQjUjA">List of countries</a> for name codes.

	       ````xml
	        <com.countrypicker.CountryCodePicker
	         android:id="@+id/ccp"
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:defaultNameCode="US"  />
	      ```` 
	      
       **Using phone code**   
        - add app:defaultCode="81" (replace 81 with your default country code) to xml layout.Refer <a href="https://goo.gl/FQjUjA">List of countries</a> for country codes.
        - Setting default country using phone code is not recommended. There are few cases where more than one countries have same phone code. Say US and Canada have +1. Putting '1' will result in Canada even if you were intended  for US.  Use app:defaultNameCode or app:countryPreference to overcome issue.
	
	       ````xml
	        <com.countrypicker.CountryCodePicker
	         android:id="@+id/ccp"
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:defaultCode="81" />
	      ````
  _app:defaultNameCode has high priority than app:defaultCode._
  
   - ####Programmatically####
       **Using country name code** 
         - Use ```` setDefaultCountryUsingNameCode()```` method.
   
       **Using phone code** 
         - To set default country programmatically, use ```` setDefaultCountryUsingPhoneCode()```` method.
    

    - ````setDefaultCountryUsingNameCode()```` or ```setDefaultCountryUsingPhoneCode() ``` will not set default country as selected country in CCP view. To set default country as selected country in CCP view, call ```` resetToDefaultCountry() ```` method.

    - ```resetToDefaultCountry() ``` will set default country as selected country in CCP, it can be used at the time of form reset.
      
    - If you do not specify default country from xml, IN +91 (India) will be the default country until you update default country programmatically.
 
    
    
  ###2. Choose and set country
  
   - Choosing and setting country will update selected country in CCP view.
    ####Choose Country
             
      1. In order to choose country, click on CCP view.
      2. Then search country by country name or phone code or name code in dialog. 
      3. Click on county from list to choose
        
     ####Set country programmatically
		
      **Using country code name**  
		- Country in CCP can be using ```` setCountryForNameCode() ```` method.

      **Using phone code**  
		- Country in CCP can be using ```` setCountryForCode() ```` method.
	
	- If specified country code / name code does not match with any country, default country will be set in to CCP.
      
     **How to listen change in selection?**
     	- To get call back when country is changed, you need to add OnCountryChangeListener from code.
	```java 
	   ccp.setOnCountryChangeListener(new CountryCodePicker.OnCountryChangeListener() {
		@Override 
		public void onCountrySelected() {
			 Toast.makeText(getContext(), "Updated " + ccp.getSelectedCountryName(), Toast.LENGTH_SHORT).show();
           	 }
       	   });
	   ```

  ###3. Country preference
  
    - Library has list of countries in alphabetical order. It searches for country in same order. But preferred country/countries have higher priority than rest.
    - There are few cases where more than one countries have same code. For example, Canada, Puerto Rico and US have +1. When lilbrary will try to find country with +1, it will always pick Canada as it's alphabetically first in (1)Canada-(2)Puerto Rico-(3)US.
    - If US is set in country preference, order for search will be (1)US-(2)Canada-(3)Puerto Rico, so it will pick US for +1.
    - Countries of preference will be listed at top in selection dialog. It is helpful when target audience is from a set of countries.
    - Any number of countries can be set in preference.
   
  - ####Set through xml####
        - Add app:countryPreference="US,IN,NZ" (replace "US,IN,NZ" with your preference) to xml layout. Refer <a href="https://goo.gl/FQjUjA">List of countries</a> for name codes.

	       ````xml
	        <com.countrypicker.CountryCodePicker
	         android:id="@+id/ccp"
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:countryPreference="US,IN,NZ"  />
	      ````
  
   - ####Programmatically####
        - Use ```` setCountryPreference()```` method.
        
  ###4. Read selected country
  
    - Country's 3 properties (Country name, phone code and name code) can be read individually.
    
     ####Read selected country phone code
    
	   - To get selected country code as String type and without prefix “+”, use ```` getSelectedCountryCode(); ```` method. => “91”
	   - To get selected country code as String type and with prefix “+”, use ```` getSelectedCountryCodeWithPlus(); ```` method. => “+91”
	   - To get selected country code as int (Integer) type, use ```` getSelectedCountryCodeAsInt(); ```` method. => 91
	    
     ####Read selected country name

	 - To get selected country’s name, use ```` getSelectedCountryName();```` => “India”
  
     ####Read selected country name code

	 - To get selected country’s name code, use ```` getSelectedCountryNameCode();```` => “IN”
   
   ###5. Full number support
     
     - Full number is combination of country code and carrier number. for example, if country code is 91 and carrier number is 8866667722 then "918866667722" or "+918866667722" is the full number.

     #### Register carrierNumberEditText
     
	    - CarrierNumberEditText is the supplementary editText in which carrier number part of full number is entered.
	    - A carrierNumberEditText must be registered in order to work with full number.
	    - editText can be registered using ``` registerCarrierNumberEditText()```.
  
     ####Load full number####
       
        - To load full number, use ```` setFullNumber()```` method. In this method you need to pass the full number.
        - Prefix “+” is optional for full number so full number can be “91886667722” or “+918866667722”. Both will set same country and carrier number."
        - This will detect country code from full number and set that county to ccp and carrier number ( remaining part of full number other than country code) will be set as text of registered carrier editText.
        - If no valid country code is found in beginning part of full number, default country will be set to CCP and full number will be set as text of registered carrier editText.
  
     ####Get full number####
     
        - Use ``` getFullNumber();``` for full number without “+” prefix.
        - Use ``` getFullNumberWithPlus();``` for full number with “+” prefix.

    - A carrierNumberEditText must be registered before any function call of full number like ``` setFullNumber()``` or ``` getFullNumber() ```.
  - *None of the above functions validate the number format of phone.*

  ###6. Custom content color
  - Color of CCP content can be changed according to different background.
    
    ####Using XML
    - Add app:contentColor property to xml layout
   
	      ````xml
	      <com.countrypicker.CountryCodePicker
	            android:layout_width="wrap_content"
	          android:layout_height="wrap_content"
	          app:contentColor="@color/custom_color"/>                        
	      ````
    
    - <img src="https://farm6.staticflickr.com/5590/30736274540_b156916b98_z.jpg" width="300">

    ####Programmatically
    - To set color programmatically, use ```` setContentColor() ```` method.
    - <img src="https://farm6.staticflickr.com/5821/30736274500_02e03a57dd_z.jpg" width="300"> 


 ###7. Custom textSize
  - Text size of CCP content can be changed in order to match rest of the view of form.
  - Everytime when textSize is updated, arrowsize will be updated itself. 
  - <img src="https://farm6.staticflickr.com/5743/30296515043_78d70ff6ba_z.jpg" width="300">  
    ####Using XML
    - Add app:contentColor property to xml layout
  
	      ````xml
	      	<com.countrypicker.CountryCodePicker
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:textSize="26sp"/>                        
	      ````

    ####Programmatically
    - To set textSize programmatically, use ```` setTextSize() ```` method.
    
 ###8. Custom arrow size
  - Size if Down arrow of CCP view can be modified in order to match rest of the view of form.
    
    ####Using XML
    - Add app:contentColor property to xml layout
	      
	````xml
	      <com.countrypicker.CountryCodePicker
	       android:layout_width="wrap_content"
	       android:layout_height="wrap_content"
	       app:arrowSize="26sp"/>                        
	  ````

    ####Programmatically
    - To set textSize programmatically, use ```` setArrowSize() ```` method.
    
 ###9. Hide country name code
  - By default, text of CCP contains coutry's name code. i.e "(US) +1". Coutnry name code can be removed if required. 
    
    ####Using XML
    - Add app:hideCodeName property to xml layout
	      
	````xml
	      <com.countrypicker.CountryCodePicker
	       android:layout_width="wrap_content"
	       android:layout_height="wrap_content"
	       app:hideNameCode="true"/>                        
	  ````

    ####Programmatically
    - To set textSize programmatically, use ```` hideNameCode() ```` method.
  
  ###10. Custom master country list
  
    - If your app expects users from only few countries then you might wish to remove all other countries from selection list.
    - You can remove unnecessary countries by setting your custom master country list.
    - Also it will keep user from selecting irrelevant country.
    - Countries of preference will be listed at top in selection dialog. It is helpful when target audience is from a set of countries.
    - Custom master list will only limit the visibility of irrelevant countries from selection dialog. But all other functions like setCountryForCodeName() or setFullNumber() will consider all the countries.
    - Preferred country list will be a subset of custom master list. If some xyz country is not in custom master list, it won't be added to preferred country list.
   
  - ####Set through xml####
        - add app:customMasterCountries="US,IN,NZ,BD,PL,RO,ZW" (replace "US,IN,NZ,BD,PL,RO,ZW" by your own country code names) to xml layout. Refer <a href="https://goo.gl/FQjUjA">List of countries</a> for name codes.

	       ````xml
	        <com.countrypicker.CountryCodePicker
	         android:id="@+id/ccp"
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:customMasterCountries="US,IN,NZ,BD,PL,RO,ZW"  />
	      ````
  
   - ####Programmatically####
        - Use ```` setCustomMasterCountries()```` method. 
        - ```` setCustomMasterCountries(null);```` will remove custom list and revert to library default list.


 ###11. Custom font
  - FontFamily of CCP content can be changed in order to match rest of the view of form.
  - Font can be set programmatically only.  
  - <img src="https://farm6.staticflickr.com/5334/31103136905_1f0dc0b535_z.jpg" width="300">  
   
    ####Programmatically
    - Step 1: create a folder named 'assets' under 'app/src/main/' folder. If you already have 'app/src/main/assets' then jump to next step.
    - Step 2: put your font's .ttf file in assets folder. For example if file name is 'myfonts.ttf', it should be 'app/src/main/assets/myfonts.ttf'. Make sure that the extension '.ttf' have contain small letters only. '.TTF' might not work.
    - Step 3: now prepare typeFace using ```` Typeface typeFace=Typeface.createFromAsset(getContext().getAssets(),"myfonts.ttf"); ````
    - Step 4: finally apply the type face on ccp ```` ccp.setTypeFace(typeFace); ```` OR ```` ccp.setTypeFace(typeFace,customStyle); ````
   
 ###12. Language support
    - Supported languages: Arabic, Bengali, Chinese, English, French, German, Gujarati, Hindi, Japanese, Javanese, Portuguese, Russian, Spanish
    - <img src="https://farm6.staticflickr.com/5444/30960801252_34b573e938_z.jpg" width="300"> 
    - More languages can be added in the future.
    - Language will be applied in country selection dialog.
    - Google translator was used to tranlate. So there is possibility of translation error, if you find any mistake please report issue to correct it or send pull request.
    - <img src="https://farm6.staticflickr.com/5738/30736274420_213808d03b_z.jpg" width="300"> 
   
  - ####Set through xml
        - add app:ccpLanguage="JAPANESE" to xml layout

	       ````xml
	        <com.countrypicker.CountryCodePicker
	         android:id="@+id/ccp"
	         android:layout_width="wrap_content"
	         android:layout_height="wrap_content"
	         app:ccpLanguage="JAPANESE"  />
	      ````
  
  - ####Programmatically
        - Use ```` changeLanguage()```` method.

 ###13. National Flag Thumbnail
     - Added flag thambnail to cpp and selector dialog
     - More thumbnail packs can be added
     - By default flag will be added to the ccp view
   - ####Set through xml
           - add app:showFlag="false" to remove flag using xml layout

   	       ````xml
   	        <com.countrypicker.CountryCodePicker
   	         android:id="@+id/ccp"
   	         android:layout_width="wrap_content"
   	         android:layout_height="wrap_content"
   	         app:showFlag="false"
   	         app:ccpLanguage="JAPANESE"  />
   	      ````

     - ####Programmatically
           - Use ```` showFlag(false)```` method to hide the flag.

 ###14. Show Full Country Name
   - Developer might wish to show full country name instead of only code name
   - `showFullName` will replace name code with full name.
   - If name code was hidden using app:hideNameCode="true" then this will not work.
   - Some country names are real long so go for this option only if your UI has dedicated enough space for it.
   - <img src="https://farm6.staticflickr.com/5514/31103136845_1abdfcfe81_z.jpg" width="300"> 
   - ####Set through xml####
              - add app:showFullName="true" to show full nameinstead of name code
	     

      	       ````xml
      	        <com.countrypicker.CountryCodePicker
      	         android:id="@+id/ccp"
      	         android:layout_width="wrap_content"
      	         android:layout_height="wrap_content"
      	         app:showFullName="true"
      	         app:ccpLanguage="JAPANESE"  />
      	      ````

   - ####Programmatically

       - Use ```` showFullName(false)```` or ```` showFullName(false)```` method to show / hide the full name.
        
Change log
--------

##### version 0.1.1
    - First upload with all basic functionalities
  
##### version 1.2
    - Support for textSize and arrowSize modification
    
##### version 1.4
    - Country preference
    - Hide country name code option
    - Default country using Country name code

##### version 1.5
    - Custom master list
    - Custom font
    - Language support
    - Optional KeyboardAutoPopup
    
##### version 1.5.1
    - Changed ccp view size when code name is hidden
    
##### version 1.6
    - Added country change listener

##### version 1.6.1
    - Bug fix for getDefaultCountryCodeAsInt() and getDefaultCountryCodeAsInt()

##### version 1.7.1
    - Adds Flag thumbnail
    - Adds option for full country name

## License

[Apache Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

    Copyright (C) 2016 Harsh Bhakta

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
