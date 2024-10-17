REPOROOT=../../..
# Use make help, to see the available rules
include $(REPOROOT)/transforms/.make.modules

#
# This is intended to be included across the Makefiles provided within
# a given transform's directory tree,  so must use compatible syntax.
#
################################################################################
# This defines the name of the transform and is used to match against
# expected files and is used to define the transform's image name. 
TRANSFORM_NAME=$(shell basename `pwd`)

################################################################################
# This defines the transforms' version number as would be used
# when publishing the wheel.  In general, only the micro version
# number should be advanced relative to the DPK_VERSION. 
#
# If you change the versions numbers, be sure to run "make set-versions" to 
# update version numbers across the transform (e.g., pyproject.toml).
#TRANSFORM_VERSION=$(DPK_VERSION)



#####################################################################################
### Example how developes can use the framework to setup the environment 
### and do their own testing. The virtual environement venv can further be customized
### and tailored to their need
run-cli-sample:
	$(MAKE) .transforms.python-venv
	source venv/bin/activate && \
	$(PYTHON) -m dpk_doc_quality.transform_python \
		--data_local_config "{ 'input_folder' : '../test-data/input', 'output_folder' : '../output'}" \
           --docq_text_lang \"en\"	\
		   --docq_doc_content_column \"contents\"	\
		   --docq_bad_word_filepath \"../ldnoobw/en\"


run-cli-sample-ray: 
	$(MAKE) .transforms.ray-venv
	source venv/bin/activate && \
	$(PYTHON) -m dpk_doc_quality.ray.transform \
		--data_local_config "{ 'input_folder' : '../test-data/input', 'output_folder' : '../output'}" \
           --docq_text_lang \"en\"	\
		   --docq_doc_content_column \"contents\"	\
		   --docq_bad_word_filepath \"../ldnoobw/en\"


run-cli-local-ray: 
	$(MAKE) .transforms.ray-venv
	source venv/bin/activate && \
	$(PYTHON) -m dpk_doc_quality.ray.local