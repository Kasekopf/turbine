FROM python:3.7

RUN pip install turbine

# Run the turbine worker
ENTRYPOINT ["python", "-c", "import turbine; turbine.run()"]