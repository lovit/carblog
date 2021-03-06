# Scrapping postprocessor: Selecting intended documents from topically various blogs

웹공간에서 블로그 데이터를 스크래핑 할 경우에 query를 검색엔진에 넣어 해당 단어가 포함되어 있는 문서들을 가져옵니다. 그 뒤, 특정 단어가 들어간 문서들을 제거하는 형식의 후처리과정을 거칩니다. 

자동차 관련 블로그를 수집할 경우, ['제네시스', '소나타', '티구안']과 같은 query를 넣을 수 있지만, '제네시스'에는 영화 '터미네이터: 제네시스'가, '소나타'의 경우에는 음악 관련 블로그가 함께 검색될 수 있습니다. 특정 단어가 들어간 문서를 제거하는 방법은 우리가 '터미네이터'가 '제네시스'에, '악장'이란 단어가 '소나타'의 블로그에 포함될 것이라 사전에 알 경우에 이용할 수 있습니다. 하지만, 우리가 준비하는 dictionary of negative words는 실제 negative documents를 모두 다룰 수 있는 수준이라 장담할 수 없습니다. 

우리는, 이 문제를 해결하기 위하여 **데이터 기반으로 negative documents를 분리** 할 것입니다.

## Script

For tokenizer training, 

	python training_tokenizer.py --corpus_directory /YOUR_CORPUS_DIRECTORY --tokenizer_type droprate --tokenizer_fname YOUR_TOKENIZER_FILE_NAME --min_frequency 100

tokenizer training parameters

	--subword_max_length (default 8)
	--minimum_droprate_score (default 0.4)
	--minimum_branching_entropy (default 1.5)
	--num_units_of_wpm (default 5000)

For (subword, document frequency ratio) table,

	python making_df_distribution.py --corpus_directory /YOUR_CORPUS_DIRECTORY --tokenizer_type droprate --tokenizer_fname YOUR_TOKENIZER_FILE_NAME --distribution_fname YOUR_RESULT_FILE_NAME


