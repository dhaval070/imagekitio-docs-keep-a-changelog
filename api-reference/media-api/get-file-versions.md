# Get all versions of a file

{% swagger baseUrl="https://api.imagekit.io" path="/v1/files/:fileId/versions" method="get" summary="Get file version details API" %}
{% swagger-description %}
Get all the file version details and attributes of a file.
{% endswagger-description %}

{% swagger-parameter in="path" name="fileId" type="string" required="true" %}
The unique fileId of the uploaded file. `fileId` is returned in list files API and upload API.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
base64 encoding of `your_private_api_key:`

**Note the colon in the end.**
{% endswagger-parameter %}

{% swagger-response status="200" description="An array of file objects is returned." %}
```javascript
[
    {
        "fileId": "598821f949c0a938d57563bd",
        "type": "file-version",
        "name": "file1.jpg",
        "filePath": "/images/products/file1.jpg",
        "tags": ["t-shirt", "round-neck", "sale2019"],
        "AITags": [
            {
                "name": "Shirt",
                "confidence": 90.12,
                "source": "google-auto-tagging"
            },
            /* ... more googleVision tags ... */
        ],
        "versionInfo": {
                "id": "697821f849c0a938d57563ce",
                "name": "Version 2"
        },
        "isPrivateFile": false,
        "customCoordinates": null,
        "url": "https://ik.imagekit.io/your_imagekit_id/images/products/file1.jpg?ik-obj-version=bREnN9Z5VQQ5OOZCSvaXcO9SW.su4QLu",
        "thumbnail": "https://ik.imagekit.io/your_imagekit_id/tr:n-media_library_thumbnail/images/products/file1.jpg?ik-obj-version=bREnN9Z5VQQ5OOZCSvaXcO9SW.su4QLu",
        "fileType": "image",
        "mime": "image/jpeg",
        "width": 100,
        "height": 100,
        "size": 100,
        "hasAlpha": false,
        "customMetadata": {
            brand: "Nike",
            color: "red"
        },
        "createdAt": "2019-08-24T06:14:41.313Z",
        "updatedAt": "2019-09-24T06:14:41.313Z"
    },
    ...more items
]
```
{% endswagger-response %}

{% swagger-response status="404" description="If the requested asset is not found in the media library, then a 404 response is returned." %}
```javascript
{
     "message" : "The requested asset does not exist.",
     "help" : "For support kindly contact us at support@imagekit.io ."
}
```
{% endswagger-response %}
{% endswagger %}

### Response structure and status code (application/JSON)

In case of an error, you will get an [error code](../api-introduction/#error-codes) along with the error message. On success, you will receive a `200` status code with the [file object](./#file-object-structure) in JSON-encoded response body.

## Examples

Here is the example request to understand the API usage.

{% tabs %}
{% tab title="cURL" %}
```bash
# The unique fileId of the uploaded file. fileId is returned in response of list files API and upload API.
curl -X GET "https://api.imagekit.io/v1/files/fileId/versions" \
-u your_private_api_key:
```
{% endtab %}
{% tab title="Go" %}
```Go
resp, err := ik.Media.AssetVersions(ctx, media.AssetVersionsParam{
    FileId: fileId,
})
```
{% endtab %}
{% endtabs %}
