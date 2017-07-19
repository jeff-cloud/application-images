all: spark zeppelin
push: push-spark push-zeppelin
.PHONY: push push-spark push-zeppelin spark zeppelin zeppelin-build

# To bump the Spark version, bump the spark_ver in Dockerfile, bump
# this tag and reset to v1. You should also double check the native
# Hadoop libs at that point (we grab the 2.6.1 libs, which are
# appropriate for 1.5.2-with-2.6). Note that you'll need to re-test
# Zeppelin (and it may not have caught up to newest Spark).
TAG = 2.1.1_v1

# To bump the Zeppelin version, bump the version in
# zeppelin/Dockerfile and bump this tag and reset to v1.
ZEPPELIN_TAG = v0.7.2_v1

spark:
	docker build -t databeanau/spark .
	docker tag databeanau/spark databeanau/spark:$(TAG)
	docker tag databeanau/spark databeanau/spark-base

# This target is useful when needing to use an unreleased version of Zeppelin
zeppelin-build:
	docker build -t databeanau/zeppelin-build zeppelin-build
	docker tag databeanau/zeppelin-build databeanau/zeppelin-build:$(ZEPPELIN_TAG)

zeppelin:
	docker build -t databeanau/zeppelin zeppelin
	docker tag databeanau/zeppelin  databeanau/zeppelin:$(ZEPPELIN_TAG)

push-spark: spark
	docker push databeanau/spark
	docker push databeanau/spark:$(TAG)

push-zeppelin: zeppelin
	docker push databeanau/zeppelin
	docker push databeanau/zeppelin:$(ZEPPELIN_TAG)

clean:
	docker rmi databeanau/spark:$(TAG) || :
	docker rmi databeanau/spark || :

	docker rmi databeanau/zeppelin:$(ZEPPELIN_TAG) || :
	docker rmi databeanau/zeppelin || :
