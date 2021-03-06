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
