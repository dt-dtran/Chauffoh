FROM python:3.10-bullseye as production
RUN python -m pip install --upgrade pip
WORKDIR /app

# Copy the top-level files in your service's directory
# Modify these instructions to do that
COPY api/requirements.txt .
COPY api/main.py .
COPY api/authenticator.py .

# Copy all of the subdirectories in your service's directory
# Modify these instructions to do that
COPY ./api/queries/ ./queries/
COPY ./api/router/ ./router/

RUN python -m pip install --no-cache-dir -r requirements.txt
EXPOSE 8000

ENV CORS_HOST https://rent-a-driver1.gitlab.io/module3-project-gamma
ARG DATABASE_URL
ENV DATABASE_URL=${DATABASE_URL}
ENV SIGNING_KEY=${SIGNING_KEY}

# !! PORT env var needs to match with exposed port in caprover dashboard
# CMD uvicorn main:app --host 0.0.0.0 --port 80


# If you're using a relational database and want migrations
# to be run automatically, delete the previous CMD line and
# uncomment the following COPY and CMD lines
COPY ./api/migrations/ ./migrations
# # !! PORT env var needs to match with exposed port in caprover dashboard
CMD python -m ./migrations/ up && uvicorn main:app --host 0.0.0.0 --port 80
