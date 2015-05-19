Python-based client library for HydroShare REST API

Questions? brian_miles@unc.edu

# To run tests (Coming soon!!!)
    python setup.py test

# To use

To get system metadata for public resources:

    from hs_restclient import HydroShare
    hs = HydroShare()
    for resource in hs.getResourceList():
        print(resource)

To authenticate, and then get system metadata for resources you have access to:

    from hs_restclient import HydroShare, HydroShareAuthBasic
    auth = HydroShareAuthBasic(username='myusername', password='mypassword')
    hs = HydroShare(auth=auth)
    for resource in hs.getResourceList():
        print(resource)

To connect to a development HydroShare server:

    from hs_restclient import HydroShare
    hs = HydroShare(hostname='mydev.mydomain.net', port=8000)
    for resource in hs.getResourceList():
        print(resource)

To get the system metadata for a particular resource:

    from hs_restclient import HydroShare
    hs = HydroShare()
    resource = hs.getResource('e62a438bec384087b6c00ddcd1b6475a')
    print(resource['resource_title'])
    
To get the BagIt archive of a particular resource:

    from hs_restclient import HydroShare
    hs = HydroShare()
    hs.getResourceBag('e62a438bec384087b6c00ddcd1b6475a', destination='/tmp')
    
or to have the BagIt archive unzipped for you:

    from hs_restclient import HydroShare
    hs = HydroShare()
    hs.getResourceBag('e62a438bec384087b6c00ddcd1b6475a', destination='/tmp', unzip=True)

or to get the BagIt archive as a generator (sort of like a buffered stream):

    from hs_restclient import HydroShare
    hs = HydroShare()
    resource = hs.getResourceBag('e62a438bec384087b6c00ddcd1b6475a')
    with open('/tmp/myresource.zip', 'wb') as fd:
        for chunk in resource:
            fd.write(chunk)