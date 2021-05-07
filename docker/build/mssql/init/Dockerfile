# escape=`

ARG BASE_IMAGE
ARG SXA_IMAGE
ARG SPE_IMAGE
# ARG HORIZON_RESOURCES_IMAGE

FROM ${SPE_IMAGE} AS spe_resources

FROM ${SXA_IMAGE} AS sxa_resources

FROM ${BASE_IMAGE} AS spe

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

COPY --from=spe_resources C:\module\db C:\resources\spe

FROM spe AS sxa

COPY --from=sxa_resources C:\module\db C:\resources\sxa

FROM sxa AS cxa

COPY ./dacpacs ./resources

