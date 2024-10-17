ARG BASE_IMAGE=docker.io/rayproject/ray:2.24.0-py310
ARG TRANSFORM_NAME
ARG WHEEL_FILE_NAME

FROM ${BASE_IMAGE}

RUN pip install --upgrade --no-cache-dir pip 

# install pytest
RUN pip install --no-cache-dir pytest

# Copy and install data processing libraries 
# These are expected to be placed in the docker context before this is run (see the make image).
COPY --chown=ray:users lib-dist/${WHL_FILE_NAME} dist/
RUN pip install dist/${WHEEL_FILE_NAME}[ray]

COPY --chown=ray:users requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY --chown=ray:users dpk_${TRANSFORM_NAME}/ dpk_${TRANSFORM_NAME}/

# copy some of the samples in
#COPY ./src/doc_quality_local_ray.py local/

# copy test
COPY test/ test/
COPY test-data/ test-data/

# Set environment
ENV PYTHONPATH /home/ray

# Put these at the end since they seem to upset the docker cache.
ARG BUILD_DATE
ARG GIT_COMMIT
LABEL build-date=$BUILD_DATE
LABEL git-commit=$GIT_COMMIT
