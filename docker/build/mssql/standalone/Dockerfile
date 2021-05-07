# escape=`

ARG BASE_IMAGE
ARG SXA_IMAGE
ARG SPE_IMAGE
# ARG HORIZON_RESOURCES_IMAGE

FROM ${SPE_IMAGE} AS spe_resources

FROM ${SXA_IMAGE} AS sxa_resources

# FROM ${HORIZON_RESOURCES_IMAGE} as horizon_resourses

FROM ${BASE_IMAGE} AS spe

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

COPY --from=spe_resources C:\module\db C:\spe_data

RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\spe_data; `
    Remove-Item -Path C:\spe_data -Recurse -Force;

FROM spe AS sxa

COPY --from=sxa_resources C:\module\db C:\sxa_data

RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\sxa_data; `
    Remove-Item -Path C:\sxa_data -Recurse -Force;

COPY dacpacs/ C:/commerce_data

RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\commerce_data; `
    Remove-Item -Path C:\commerce_data -Recurse -Force;


# Add Horizon module
# COPY --from=horizon_resourses \module\db \horizon_integration_data

# RUN C:\DeployDatabases.ps1 -ResourcesDirectory C:\horizon_integration_data; `
#     Remove-Item -Path C:\horizon_integration_data -Recurse -Force;

