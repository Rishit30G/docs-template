---
title: Offline Data Synchronization ☁️
sidebar_label: Offline Data Synchronization ☁️
slug: /offline-data-synchronization
hide_table_of_contents: true
# demoUrl: https://passbook.familyid.samagra.io/
demoSourceUrl: https://github.com/Samagra-Development/pwa-docs
---

<head>
  <title>Offline Data Synchronization ☁️</title>
  <meta name="description" />
</head>

- A data layer is implemented using **IndexedDB** allowing for offline data storage and synchronization with the server.
- When the app is **offline**:

  - User-entered data is saved locally in the IndexedDB database.

    <video height='500' controls>
      <source src="/assets/offline-feedback.mp4" type="video/mp4" />
    </video>

    ![IndexDB](/assets/indexDB.png)

- The app remains functional and responsive, allowing users to work with data even without an internet connection.
- When the app is back **online**:
  - The data layer detects the connectivity status.
  - Synchronization is initiated to send the locally stored data to the server.
  - Changes made offline are seamlessly synced with the central data source on the server.
- This approach ensures data consistency and provides users with a consistent experience across online and offline scenarios.
- Users can work with data even when offline, and their changes are automatically synced with the server when connectivity is restored.

## Implementation

```js
const callApi = useCallback((payload: any) => {
  if (navigator.onLine) {
    const apiObject: RequestObject = {
      url: payload.url,
      ...omit(
        {
          method: payload.method,
          data: payload.body,
          headers: payload.headers,
          queryParams: payload.queryParams,
          baseURL: payload.baseURL,
          params: payload.params,
          timeout: payload.timeout,
          responseType: payload.responseType || 'json',
        },
        function (value) {
          return isNull(value);
        }
      ),
    };
    //@ts-ignore
    return axios.request(apiObject);
  } else {
    return new Promise((resolve) => {
      appendApi(payload);
      resolve('offline');
    });
  }
}, []);
```
