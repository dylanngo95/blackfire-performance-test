# blackfire-performance-test

## Write performance test in PHP Unit

```bash

    public function testGetGitHubOrganization()
    {
        $client = static::createClient();
        $blackfireConfig = (new Configuration())
            ->assert('metrics.http.requests.count == 1');
            
        $blackfireConfig = (new Configuration())
            ->assert('metrics.http.requests.count == 1');
        $this->assertBlackfire($blackfireConfig, function() use ($client) {
            $client->request('GET', '/api/github-organization');
            $this->assertResponseIsSuccessful();
            $data = json_decode($client->getResponse()->getContent(), true);
            $this->assertArrayHasKey('organization', $data);
        });
    }
    
```
# Write scenarios in .blackfire.yaml

```bash
scenarios: |
    #!blackfire-player
    scenario
        name "Basic Visit"
        visit url('/')
            name "Homepage"
            expect status_code() == 200
            expect css("tbody.js-sightings-list tr").count() > 10
            # won't work until we're using Blackfire environment
            assert metrics.sql.queries.count 
        click link("Log In")
            name "Log in page"
            expect status_code() == 200
            
            blackfire-player run .blackfire.yaml --ssl-no-verify --endpoint=https://localhost:8000

```
