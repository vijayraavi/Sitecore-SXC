# escape=`

ARG BASE_IMAGE
ARG SXA_IMAGE

FROM ${SXA_IMAGE} AS sxa_resources
FROM ${BASE_IMAGE} AS sxa

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Add SXA module
COPY --from=sxa_resources C:\module\solr\cores-sxa.json C:\data\cores-sxa.json