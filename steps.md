---
author: Hazem Hemied
description: This documentation help building quay for enterprise customers, can be used for a demo or a POC.
categories:
  - docs
  - demos
tags:
  - quay
status: done
published: true
---

# Quay 3.6

# Steps:`

- **_Important links_**
  [Add proxy variables to Clair - Red Hat Customer Portal](https://access.redhat.com/solutions/6435091)
  [Early access documentation for Red Hat Quay 3.7.0](https://stevsmit.github.io/quay-docs/eap-directory/html-single/)
  [Chapter 2. Configuration fields Red Hat Quay 3.6 | Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_quay/3.6/html/configure_red_hat_quay/config-fields-intro#config-preconfigure-automation-intro)
- install quay registry operator
  > The steps is available in the documentations
- create quay namespace
  ```bash
  oc new-project quay
  ```
- create bundle secrets

  ```yaml
  ---
  -----BEGIN CERTIFICATE-----
  MDIxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MQswCQYDVQQD
  EwJSMzAeFw0yMjA0MDcxNzU4MTZaFw0yMjA3MDYxNzU4MTVaMCAxHjAcBgNVBAMT
  FXF1YXkub3BlbnNoaWZ0NG1lLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
  AQoCggEBAOtuiPCjaI+MIMKN3S2dY/J/3e2BwTqgcVdAqtfFJuoIYyWxmg31RJJ8
  EuFv3iblj+mXqsxKP4arX22Avu7De2qCLUFL4Q/3oPF3HDAxfBJifGpqaXq2ij/O
  CLlLWEVDQxrocEsS+XGsvIlwy7PzqZ5D+JeKKHgWzsCxjci19QIJHsmpw/GCoi0u
  ok5J2C4DG5T0oalAwEAAaOCAk8wggJLMA4GA1UdDwEB/wQE
  AwIFoDAdBgNVHSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIwDAYDVR0TAQH/BAIw
  ADAdBgNVHQ4EFgQU1FFjwXFrqByH35oDvRCMtUz7vXwwHwYDVR0jBBgwFoAUFC6z
  F7dYVsuuUAlA5h+vnYsUwsYwVQYIKwYBBQUHAQEESTBHMCEGCCsGAQUFBzABhhVo
  dHRwOi8vcjMuby5sZW5jci5vcmcwIgYIKwYBBQUHMAKGFmh0dHA6Ly9yMy5pLmxl
  bmNyLm9yZy8wIAYDVR0RBBkwF4IVcXVheS5vcGVuc2hpZnQ0bWUuY29tMEwGA1Ud
  IARFMEMwCAYGZ4EMAQIBMDcGCysGAQQBgt8TAQEBMCgwJgYIKwYBBQUHAgEWGmh0
  dHA6Ly9jcHMubGV0c2VuY3J5cHQub3JnMIIBAwYKKwYBBAHWeQIEAgSB9ASB8QDv
  AHYARqVV63X6kSAwtaKJafTzfREsQXS+/Um4havy/HD+bUcAAAGABWQ73wAABAMA
  RzBFAiBTFDziWKYF2Cv7//rqrTtC6WflZImLltZvaAqp72ntbgIhAJh3jmp4TeHc
  1tzcb+wyM/w8yMFQchTMU8Wis9k7PPB4AHUAQcjKsd8iRkoQxqE6CUKHXk4xixsD
  6+tLx2jwkGKWBvYAAAGABWQ9swAABAMARjBEAiBsvZL0G5PoyPq/dndrLwZ6iOvi
  ym85Xbc5MzmVSVdhOwIgBH8jiI6H1W+AvkC53wyKGoLoBysWhWnGKA6q3V+MTFcw
  DQYJKoZIhvcNAQELBQADggEBAK3XKjCO18Zo6g6T8Vp3ebmfYY044AJGiT9v+B9V
  7HRv82kdH4V5aH4X1xvMp66hAhjC+GaWGZr0WkFpQS7Ddoi7bLd0HIMPGRZW9mz1
  owBTUTv4BBIy+yXv9zDRQqSMw5o/VM9hJyOSBDDje8+8YewCMFeNvdxRlaj9K3kW
  cH0/d1ZCGnqwwzIiNXP570OJTUi8q0p9T2tY0ERYgboI9rF2idbwE2wHe4SafDJM
  ED9AanQAIHEKo0JoXvT9xXuCjmojImmVMgrR+3pr3IP0ywyc3FXk3nDyR2QYSo/f
  TbdsYd+NDPxvI6fCXv6fbdFH3InD6OPdW+IBKPbMDOkVVNU=
  -----END CERTIFICATE-----
  -----BEGIN CERTIFICATE-----
  TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
  cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwHhcNMjAwOTA0MDAwMDAw
  WhcNMjUwOTE1MTYwMDAwWjAyMQswCQYDVQQGEwJVUzEWMBQGA1UEChMNTGV0J3Mg
  RW5jcnlwdDELMAkGA1UEAxMGjggEIMIIBBDAOBgNVHQ8BAf8EBAMC
  AYYwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUFBwMBMBIGA1UdEwEB/wQIMAYB
  Af8CAQAwHQYDVR0OBBYEFBQusxe3WFbLrlAJQOYfr52LFMLGMB8GA1UdIwQYMBaA
  FHm0WeZ7tuXkAXOACIjIGlj26ZtuMDIGCCsGAQUFBwEBBCYwJDAiBggrBgEFBQcw
  AoYWaHR0cDovL3gxLmkubGVuY3Iub3JnLzAnBgNVHR8EIDAeMBygGqAYhhZodHRw
  Oi8veDEuYy5sZW5jci5vcmcvMCIGA1UdIAQbMBkwCAYGZ4EMAQIBMA0GCysGAQQB
  gt8TAQEBMA0GCSqGSIb3DQEBCwUAA4ICAQCFyk5HPqP3hUSFvNVneLKYY611TR6W
  PTNlclQtgaDqw+34IL9fzLdwALduO/ZelN7kIJ+m74uyA+eitRY8kc607TkC53wl
  ikfmZW4/RvTZ8M6UK+5UzhK8jCdLuMGYL6KvzXGRSgi3yLgjewQtCPkIVz6D2QQz
  CkcheAmCJ8MqyJu5zlzyZMjAvnnAT45tRAxekrsu94sQ4egdRCnbWSDtY7kh+BIm
  lJNXoB1lBMEKIq4QDUOXoRgffuDghje1WrG9ML+Hbisq/yFOGwXD9RiX8F6sw6W4
  avAuvDszue5L3sz85K+EC4Y/wFVDNvZo4TYXao6Z0f+lQKc0t8DQYzk1OXVu8rp2
  yJMC6alLbBfODALZvYH7n7do1AZls4I9d1P4jnkDrQoxB3UqQ9hVl3LEKQ73xF1O
  yK5GhDDX8oVfGKF5u+decIsH4YaTw7mP3GFxJSqv3+0lUFJoi5Lc5da149p90Ids
  hCExroL1+7mryIkXPeFM5TgO9r0rvZaBFOvV2z0gp35Z0+L4WPlbuEjN/lxPFin+
  HlUjr8gRsI3qfJOQFy/9rKIJR0Y/8Omwt/8oTWgy1mdeHmmjk7j1nYsvC9JSQ6Zv
  MldlTTKB3zhThV1+XWYp6rjd5JW1zbVWEkLNxE7GJThEUG3szgBVGP7pSWTUTsqX
  nLRbwHOoq7hHwg==
  -----END CERTIFICATE-----

  -----BEGIN CERTIFICATE-----
  MSQwIgYDVQQKExtEaWdpdGFsIFNpZ25hdHVyZSBUcnVzdCBDby4xFzAVBgNVBAMT
  DkRTVCBSb290IENBIFgzMB4XDTIxMDEyMDE5MTQwM1oXDTI0MDkzMDE4MTQwM1ow
  TzELMAkGA1UEBhMCVVMxKTAnBgNVBAoTIEludGVybmV0IFNlY3VyaXR5IFJlc2Vh
  cmNoIEdyb3VwMRUwEwYDVQQDEwxJU1JHIFJvb3QgWDEwggIiMA0GCSqGSIb3DQEB
  AQUAA4ICDwAwggIKAoICAQCt6CRz9BQ385ueK1coHIe+3LffOJCMbjzmV6B493XC
  ov71am72AE8o295ohmxEk7axY/0UEmu/H9LqMZshftEzPLpI9d1537O4/xLxIZpL
  wYqGcWlKZmZsj348cL+tKSIG8+TA5oCu4kuPt5l+lAOf00eXfJlII1PoOK5PCm+D
  LtFJV4yAdLbaL9A4jXsDcCEbdfIwPPqPrt3aY6vrFk/CjhFLfs8L6P+1dy70sntK
  4EwSJQxwjQMpoOFTJOwT2e4ZvxCzSow/iaNhUd6shweU9GNx7C7ib1uYgeGJXDR5
  bHbvO5BieebbpJovJsXQEOEO3tkQjhb7t/eo98flAgeYjzYIlefiN5YNNnWe+w5y
  sR2bvAP5SQXYgd0FtCrWQemsAXaVCg/Y39W9Eh81LygXbNKYwagJZHduRze6zqxZ
  Xmidf3LWicUGQSk+WT7dJvUkyRGnWqNMQhi9odHRwOi8vYXBwcy5pZGVudHJ1
  c3QuY29tL3Jvb3RzL2RzdHJvb3RjYXgzLnA3YzAfBgNVHSMEGDAWgBTEp7Gkeyxx
  +tvhS5B1/8QVYIWJEDBUBgNVHSAETTBLMAgGBmeBDAECATA/BgsrBgEEAYLfEwEB
  ATAwMC4GCCsGAQUFBwIBFiJodHRwOi8vY3BzLnJvb3QteDEubGV0c2VuY3J5cHQu
  b3JnMDwGA1UdHwQ1MDMwMaAvoC2GK2h0dHA6Ly9jcmwuaWRlbnRydXN0LmNvbS9E
  U1RST09UQ0FYM0NSTC5jcmwwHQYDVR0OBBYEFHm0WeZ7tuXkAXOACIjIGlj26Ztu
  MA0GCSqGSIb3DQEBCwUAA4IBAQAKcwBslm7/DlLQrt2M51oGrS+o44+/yQoDFVDC
  5WxCu2+b9LRPwkSICHXM6webFGJueN7sJ7o5XPWioW5WlHAQU7G75K/QosMrAdSW
  9MUgNTP52GE24HGNtLi1qoJFlcDyqSMo59ahy2cI2qBDLKobkx/J3vWraV0T9VuG
  WCLKTVXkcGdtwlfFRjlBz4pYg1htmf5X6DYO8A4jqv2Il9DjXA6USbW1FzXSLr9O
  he8Y4IWS6wY7bCkjCWDcRQJMEhg76fsO3txE+FiYruq9RUWhiF1myv4Q6W+CyBFC
  Dfvp7OOGAN6dEOM4+qR9sdjoSYKEBpsr6GtPAQw4dy753ec5
  -----END CERTIFICATE-----
  ```

  ```bash
  -----BEGIN PRIVATE KEY-----
  jd0tnWPyf93tgcE6oHFXQKrXxSbqCGMlsZoN9USSfBLhb94m5Y/pl6rMSj+Gq19t
  gL7uw3tqgi1BS+EP96DxdxwwMXwSYnxqaml6too/zgi5S1hFQ0Ma6HBLEvlxrLyJ
  cMuz86meQ/iXiih4Fs7AsY3ItfUCCR7JqcPxgqItLqJOSdguAxuU9KGpbGQAa9cV
  vjuEFwk84QhnflobYTxsTAYXZQJbtM9dM1MHhQktWJ2VZ/ZpFcWj9rmuJsW2O52z
  f+tDTZidr6SgRH3TCboKCmK8Ju4Q8UAKW48nTcg+y0n3VbohrOJ7HeiSUvjrKNYX
  pqneGzBjAgMBAAECggEBANMu9LF+sxVIqj46iPMY4oWtQ0KACPdw4hpVTKp+E9kM
  qvst47Wvk9Ieb8U+1rRnaX8s6C2WUIOZh+EvApYkTbmNidCvovPyubC/mk50pQnM
  xDOkvncv9LUlONgViNmgazpg1BHTtGPOgdR7lI4X/MeVyxEMAh8uvklFO5yV82/d
  S9E31Oo88LjN4l6PSyaxFXMBJt07wztb3L3imOhrXr9RqY+uAMuoBj2tFUjpRP6I
  ce8mexiwL8QRnQdZXPVVTvxP23b81RjaB1PomP8rOJBuJl4HRQRF8J9j2Wl36s8y
  TW/S4uD46Avb0JAOgqo/JrAvXqJJknQEhLJqSL3JDvECgYEA/Ysbl2AlLXRxOzVD
  QTE1OSxcEcBq8qzsYvER/aMQT8e3XQeFgWzPveEnHFOf3QUFYQiUkRHVkOC0G
  qMlLDv+kHFb9adupuZv9PwZJa3Y2JpYolXIpFp7IHe8SJ9rjBU8AlibsLqGUUQi0
  KomLn4kP5vWfBkukC8tBBBnH+xG511mWtrhm+qKhOn+EWyFC0FzpM7zSEQKBgCE2
  v9QJna4NFCgGurmMQfwee60mLPpO0/36Cji9p3JavdWJh0+jkcbhtd6afEYbbKQ2
  lVw1rxb/Ffi9ehqhB6Q6m3Ze56xrHSMdlnbMHTpGhbsHcxFb/crVXC0nb9zrPbPf
  gwTedFK5hIQu7vlVozGlB3NeK1qnWp5+TaMpxsezAoGBAOPkh9ZLRWoCNZ3a2jk9
  okZ/qDsYItaZIiO+nWJllWIZIb8mHPCTzp+R7y6XOpeMQ9kIheJQNzBvXsE4zZ79
  Ru4kcn6zMqfogtOk5XwxpdcxWPuxANwkd3/D0YEMW3Y7cI6DITA9pBRbu6ATkVBD
  XZIa07e+wNRTt/E8ydkYEKZP
  -----END PRIVATE KEY-----
  ```

  ```yaml
  FFEATURE_USER_INITIALIZE: true
  BROWSER_API_CALLS_XHR_ONLY: false
  FEATURE_USER_CREATION: true
  SUPER_USERS:
    - quayadmin
    - hemied
  DISTRIBUTED_STORAGE_CONFIG:
    s3Storage:
      - S3Storage
      - host: s3.eu-central-1.amazonaws.com
        s3_access_key: AKIA6ENxxx
        s3_secret_key: xxxTHzGQpKz50r
        s3_bucket: quay-bucket
        storage_path: /datastorage/registry
  DISTRIBUTED_STORAGE_DEFAULT_LOCATIONS: []
  DISTRIBUTED_STORAGE_PREFERENCE:
    - s3Storage
  EXTERNAL_TLS_TERMINATION: false
  SERVER_HOSTNAME: quay.mydomain.com
  PREFERRED_URL_SCHEME: https
  ```

  ```bash
  oc create secret generic config-bundle-secret --from-file config.yaml --from-file ssl.cert --from-file ssl.key
  ```

- create the route
  ```yaml
  apiVersion: route.openshift.io/v1
  kind: Route
  metadata:
    annotations:
      quay-buildmanager-hostname: ""
      quay-managed-fieldgroups: "SecurityScanner,Database,DistributedStorage,Redis,HostSettings,RepoMirror,"
      quay-operator-service-endpoint: "http://quay-operator.openshift-operators:7071"
      quay-registry-hostname: "quay.mydomain.com"
    name: quay
    namespace: quay
    labels:
      quay-operator/quayregistry: quay
  spec:
    host: "quay.mydomain.com"
    to:
      kind: Service
      name: quay-quay-app
      weight: 100
    port:
      targetPort: https
    tls:
      termination: passthrough
      insecureEdgeTerminationPolicy: Redirect
    wildcardPolicy: None
  ```
- get the **routerCanonicalHostname** from the quay route
  ```bash
  oc get route quay -o jsonpath='{.status.ingress[0].routerCanonicalHostname}{"\n"}'
  ```
- Now, add this route as the CName in your dns
  [quay.mydomain.com](http://quay.mydomain.com) → [router-default.apps.quay-de.sandbox596.opentlc.com](http://router-default.apps.quay-de.sandbox596.opentlc.com/)
- create the quay-registry instance
  ```yaml
  apiVersion: quay.redhat.com/v1
  kind: QuayRegistry
  metadata:
    name: quay
  spec:
    components:
      - managed: true
        kind: clair
      - managed: true
        kind: postgres
      - managed: false
        kind: objectstorage
      - managed: true
        kind: redis
      - managed: true
        kind: horizontalpodautoscaler
      - managed: false
        kind: route
      - managed: true
        kind: mirror
      - managed: true
        kind: monitoring
      - managed: false
        kind: tls
    configBundleSecret: config-bundle-secret
  ```
- To add proxy to **Clair** and **Mirror** deployment
  You need to add the proxy to the deployment itself by adding the container environmental variables
  ```yaml
  spec:
    containers:
      - env:
          - name: HTTP_PROXY
            value: http://ta2ocp1:reM2.intranet.company.com:8080
          - name: HTTPS_PROXY
            value: http://ta2ocp1:reM2.intranet.company.com:8080
          - name: NO_PROXY
            value: <get it from oc get proxy cluster>
          - name: CLAIR_CONF
            value: /clair/config.yaml
          - name: CLAIR_MODE
            value: combo
  ```
- To add custom **proxy** certificate and configuration
  - Add the proxy certificate as a secret
    ```yaml
    oc create secret generic clair-proxy-ca --from-file ssl.cert --from-file ssl-key --from-file proxy-cert.crt
    ```
  - Add the proxy certificate secret to the deployment
    ```yaml
    volumes:
      - name: certificates
        projected:
          defaultMode: 420
          sources:
            - secret:
                name: clair-proxy-ca
    ```
- Update the registry configuration
  you can whether patch the secret from the ui or overwrite it from command line
  To enforce the operator to take effect
  1. scale the operator down and then up
  2. for testing we can add a new super user
