Python SDK for Cogniac Public API

Supported Python versions: Python 2.7 and Python 3

This client library provides access to most of the common functionality of the Cogniac public API.

## Installation
pip install cogniac

## Usage
The main entry point is the CogniacConnection object which is created as follows:

        CogniacConnection(username=None,
                          password=None,
                          api_key=None,
                          tenant_id=None,
                          timeout=60,
                          url_prefix="https://api.cogniac.io/")

        Create an authenticated CogniacConnection with the following credentials:
        
        username (String):            The Cogniac account username (usually an email address).
                                      If username is None, then use the contents of the
                                      COG_USER environment variable as the username.

        password (String):            The associated Cogniac account password.
                                      The password can also be supplied via the COG_PASS
                                      environment variable.

        api_key (String):             A Cogniac-issued API key that can be used as a substitute for
                                      a username+password.  The api_key can also be supplied via the
                                      COG_API_KEY environment variable.

        tenant_id (String):           Cogniac tenant_id with which to assume credentials.
                                      This is only required if the user is a member of multiple tenants.
                                      If tenant_id is None, and the user is a member of multiple tenants
                                      then use the contents of the COG_TENANT environment variable
                                      will be used as the tenant.

        url_prefix (String):          Cogniac API url prefix.
                                      Defaults to "https://api.cogniac.io/" for Cogniac CloudCore.
                                      If you are accessing an 'on-prem' version of the Cogniac system,
                                      please set this accordingly (e.g. 'https://your_company_name.local.cogniac.io/'
                                      or a custom DNS prefix assigned by your internal IT.)
                                      The url_prefix can alternatively be set via the COG_URL_PREFIX environment variable.
                                      
        If a user is a member of multiple tenants the user can retrieve his list of associated
        tenants via the CogniacConnection.get_all_authorized_tenants() classmethod.

Environment Variables:

    The CogniacConnection can be configured using the following environment variables:

    COG_USER               Cogniac system username (usually an email address)
    COG_PASS               Cogniac user password
    COG_API_KEY            Cogniac system API Key associated with an individual Cogniac system user
                           (Alternative to username/password)
    COG_TENANT             Cogniac system tenant_id
    COG_URL_PREFIX         Cogniac system API end-point of the form "https://FQDN/API_VERSION"


CogniacConnection has a number of helper functions for working with Cogniac
common Cogniac objects such as applications, subjects, and media:
        
    get_all_applications
        return CogniacApplications for all applications belonging to the currently authenticated tenant

    get_application
        return an existing CogniacApplication

    create_application
        Create a new CogniacApplication

    get_all_subjects
        return CogniacSubjects for all subjects belonging to the currently authenticated tenant

    get_subject
        return an existing CogniacSubject
        
    create_subject
        Create a CogniacSubject

    get_media
        return CogniacMedia object for an existing media item
        
    create_media
        create a new Cogniac media item

    get_tenant
        return the currently authenticated CogniacTenant


CogniacApplication

    An object representing an Application in the Cogniac System.
    
    Applications are the main focus of activity within the Cogniac System.

    This class manages applications within the Cogniac System via the
    Cogniac public API application endpoints.

    Create a new application with
    CogniacConnection.create_application() or CogniacApplication.create()

    Get an existing application with
    CogniacConnection.get_application() or CogniacApplication.get()

    Get all tenant's applications with
    CogniacConnection.get_all_applications() or CogniacApplication.get_all()

    Writes to mutable CogniacApplication attributes are saved immediately via the Cogniac API.


 CogniacSubject
 
    An object representing a Subject in the Cogniac System.
    
    Subjects are a central organizational mechanism in the Cogniac system.
    A subject is any user-defined concept that is relevant to images or video.
    More generally a subject can represent any logical grouping of images or video.

    Most Cogniac applications work by taking input media from user-defined subjects
    and outputing those media to other user-defined subjects based on the content
    of the media.

    Create a new subject with
    CogniacConnection.create_subject() or CogniacSubject.create()

    Get an existing subject with
    CogniacConnection.get_subject() or CogniacSubject.get()

    Get all tenant's subject with
    CogniacConnection.get_all_subjects() or CogniacSubject.get_all()

    Writes to mutable CogniacSubjects attributes are saved immediately via the Cogniac API.


CogniacMedia

    CogniacMedia objects contain metadata for media files that has been input into the Cogniac System.
    New CogniacMedia can be created by specifying a local filename containing a still image or video.
    Existing CogniacMedia can be retrieved by media_id.


CogniacTenant

    An object representing a Tenant in the Cogniac System


Example Usage:

        import cogniac

        cc = cogniac.CogniacConnection()

        print cc.get_tenant()

        print cc.get_all_applications()

        print cc.get_all_subjects()

or to run ipython with extra magic commands:

        % icogniac [optional partial tenant name or tenant_id]

        print cc.tenant_id
                        
        %media_detections <media_id>
        
        %media_subjects <media_id>


cogupload

     A utility for robust parallel upload of media to the Cogniac system. Currently this is suitable for uploading to an 'input' subject since it does not set the consensus flag.

     usage: cogupload <subject_uid> <directory_name>


## Support
Please email us at support@cogniac.co with your feedback and thoughts about this library.
