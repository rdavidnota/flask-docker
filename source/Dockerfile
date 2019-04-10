FROM python:3.7-alpine AS base
WORKDIR /app
EXPOSE 5000

FROM python:3.7-alpine AS build
COPY ["requirements.txt", "."]
WORKDIR /packages/
RUN pip download -r /requirements.txt

FROM base AS final
WORKDIR /app/packages/
COPY --from=build /packages .
RUN pip install --no-index --find-links=/app/packages/ /app/packages/*
WORKDIR /app
COPY . .
ENTRYPOINT ["python","app.py"]
