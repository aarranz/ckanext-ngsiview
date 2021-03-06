CKAN ckanext-ngsiview
=====================

[![Build Status](https://travis-ci.org/conwetlab/ckanext-ngsiview.svg?branch=ngsiv2)](https://travis-ci.org/conwetlab/ckanext-ngsiview)
[![Coverage Status](https://coveralls.io/repos/github/conwetlab/ckanext-ngsiview/badge.svg?branch=ngsiv2)](https://coveralls.io/github/conwetlab/ckanext-ngsiview?branch=ngsiv2)

CKAN extension that will give you the ability to manage real-time resources provided by a FIWARE Context Broker. This extension also provides a basic view to provide a data preview to user browsing context broker resources, altough it can be combined with other plugins (e.g. the [`ckanext-wirecloud_view`](https://github.com/conwetlab/ckanext-wirecloud_view.git) one) to provide a more advanced visualization of the data provided using CKAN.

**Note**: This extension is being tested in CKAN 2.5, 2.6 and 2.7. These are
therefore considered as the supported versions


## Requirements

* [OAuth2 CKAN Extension](https://github.com/conwetlab/ckanext-oauth2/). This extension is required to make request to secured Context Broker instances. The autentication token will be taken from the current user session, so the accessed context broker must be connected to the same IdM server as the one used to login into CKAN, if not, the token will not work.


## Installation

To install ckanext-ngsiview:

1. Activate your CKAN virtual environment, for example:

    ```
    . /usr/lib/ckan/default/bin/activate
    ```

2. Install the ckanext-ngsiview Python package into your virtual environment:

    ```
    pip install ckanext-ngsiview
    ```

3. Add `ngsiview` to the `ckan.plugins` setting in your CKAN
   config file (e.g. `/etc/ckan/default/production.ini`).

4. Restart CKAN. For example if you've deployed CKAN with Apache:

    ```
    sudo service apache2 graceful
    ```


## Development Installation

To install `ckanext-ngsiview` for development, activate your CKAN virtualenv and
do:

```
git clone https://github.com/conwetlab/ckanext-ngsiview.git
cd ckanext-ngsiview
python setup.py develop
```


## How it works


### How to create a `fiware-ngsi` resource

The way to create a NGSI resource is fairly simple:

1. Firstly you have to access to the form for creating a new resource.

   ![Create resource form](images/create_resource_form.png)

3. Use `fiware-ngsi` to fill the `Format` field, this will make the form change
   adding some extra fields required when using the `fiware-ngsi` format.

   ![Create resource after switching to the fiware-ngsi format](images/create_resource_form_fiwarengsi.png)

2. Fill the `URL` field with a Context Broker query. It is recommended to use a
   NGSIv2 query, but it is possible to use also a v1 convenience query context
   url. Examples are:

    - `http://orion.lab.fiware.org:1026/v2/entities?type=AirQualityObserved`
    - `http://orion.lab.fiware.org:1026/v1/contextEntities/MeteoLo`

3. Finally, check if you have to use some of the extra options:
    - Set the `OAuth-Token` option to `required` if the Context Broker server
        requires authentication.
    - Fill the `FIWARE-Service` field if the data is not provided by the default
        [tenant](http://fiware-orion.readthedocs.io/en/master/user/multitenancy/).
    - And finally, fill the `FIWARE-ServicePath` field if the data should be
        filtered using a [service path](http://fiware-orion.readthedocs.io/en/master/user/service_path/).

4. Once you provide all the requested information, click on the *Add* button.
