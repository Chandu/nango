import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Pagination
Nango currently supports various pagination strategies, with more in the works. 

Your favorite API is not compatible? [Open a github issue](https://github.com/NangoHQ/nango-sync/issues/new) with a link to the endpoint documentation and a sample response and we will make it work with a fast turnaround!

### Pagination Strategy 1: Next page cursor in response metadata

The API returns a cursor, in the response metadata, that points at the next page. The cursor should be passed along with the request in a special parameter (for example `after`).

Example response:
```json
{
  "results": [ ... ],
  "paging": {
    "next": {
      "after": "NTI1Cg%3D%3D",
      "link": "?after=NTI1Cg%3D%3D"
    }
  }
}
```

=> use the `paging_cursor_metadata_response_path` (here set to `paging.next.after`) and `paging_cursor_request_path` (here set to `after`) parameters in the [Sync config options](sync-all-options.md).


### Pagination Strategy 2: Next page cursor in response's last object

The API returns a cursor, in the response's last object, that points at the next page. The cursor should be passed along with the request in a special parameter (for example `after`).

Example response:
```json
{
  "results": [ 
    {
      "id": 1,
      "name": "Brad Colbert",
    },
    ...,
    {
      "id": 123,
      "name": "Josh Person",
      "cursor": "NTI1Cg%3D%3D"
    }
  ]
}
```

=> use the `paging_cursor_object_response_path` (here set to `cursor`) and `paging_cursor_request_path` (here set to `after`) parameters in the [Sync config options](sync-all-options.md).

### Pagination Strategy 3: Next page URL in response body

The API returns a URL, in the response body, where the next page of results can be fetched.

Example response body:
```json
{
    "results": [ ... ],
    "next": "https://api.example.com/docs?nextPage=2749ns92md"
}
```

=> Use the `paging_url_path` config parameter of Nango, here set to `next`, in the [Sync config options](sync-all-options.md).

### Pagination Strategy 4: Next page URL in response header

The API returns a URL, in the response's link header, where the next page of results can be fetched.

Example response header:
```json
{ "link": "'<https://api.github.com/user/2560456/repos?per_page=10&page=2>; rel=\"next\", <https://api.github.com/user/2560456/repos?per_page=10&page=3>; rel=\"last\"'" }
```

=> Use the `paging_header_link_rel` config parameter of Nango, here set to `next`, in the [Sync config options](sync-all-options.md).

## Problems with your Sync? We are here to help!

If you need help or run into issues, please reach out! We are online and responsive all day on the [Slack Community](https://nango.dev/slack).