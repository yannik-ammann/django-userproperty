#Django-UserProperty

Dajngo-UserProperty gives you the possibility to save values to a in relation to a user. There are endless possibilities for use cases.

## Installation

Install the package:

    pip install django-userproperty
    
Add the app in you settings.py:

    INSTALLED_APPS = (
        'userproperty',
    )

And finally sync your db

    python manage.py syncdb

## Usage

### Example: 



After creating an account on your website, the user needs to do some tasks before he can enter his profile. In this example adding more information and agreeing to the terms and conditions.

When creating the new user you create a new property:

    from userproperty.utils import addProperty
    
    addProperty(request, tag='setup') 
    # if the user is not saved in the request add: anUser=yourNewUser
    
In your login view you can now have different outcomes based on the UserProperty

    from userproperty.utils import getIntegerProperty, setIntegerProperty, removeProperty

    #in your login view
    
    setupProperty = getIntegerProperty(request,'setup')
    
    if setupProperty is 1:
        #redirect, a form for adding phone number etc
    elif setupProperty is 2:
        #redirect, accepting the terms and conditions
    elif setupProperty:
        removeProperty(request, tag='setup')
    
    # stuff when no property was set
    
The only thing left to do is setting the property to a new value when the respective actions(forms in this case) are done:

    from userproperty.utils import setIntegerProperty, removeProperty

    #in the view with the form for the phonenumer etc.
    form.is_valid():
        #do stuff
        
        setIntegerProperty(request, tag='setup', value=2)
        
        #redirect login
        
        
    #in the view for terms and conditions
    form.is_valid():
        #do stuff
        
        removeProperty(request, tag='setup')
        
        #redirect login

Other examples: setup tour, saving user specific properties(number of data entries displayed in js datatables), etc.

## PEP8

The functions are available in pep8 (lowercase with _ as separator between words)

setIntegerProperty() ==> set_integer_property()
