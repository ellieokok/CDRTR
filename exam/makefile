export PYTHONPATH=..

# make generatevoca MODE=DEBUG DATA=data
generatevoca:
	python -m CDRTR.preprocess generatevoca --mode $(MODE) --fields asin,reviewerID,overall,reviewText,unixReviewTime --data_dir $(DATA)

# make extractinfo MODE=DEBUG
extractinfo:
	python -m CDRTR.preprocess extractinfo --mode $(MODE)

preprocess: generatevoca extractinfo

# make sentitrain DATA=data DOMAIN=Music
# make sentitrain DATA=data DOMAIN=Auto
sentitrain:
	python -m CDRTR.core.DeepModel.SentiRec --dir $(DATA)/preprocess --domain $(DOMAIN) --filter_size 3,5,7,11 --epoches 400

mergeUI:
	python -m CDRTR.preprocess mergeui --mode $(MODE) --data_dir $(DATA)

DSNRec:
	python -m CDRTR.core.DeepModel.DSNRec --data_dir $(DATA) --src_domain $(SRCDO) --tgt_domain $(TGTDO) --epoches $(EPOCH) --mode $(MODE)
