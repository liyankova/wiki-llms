---
url: https://bun.com/reference/node/zlib
title: Node.js zlib module | API Reference | Bun
source_domain: bun.com
---

# Node.js zlib module | API Reference | Bun

Node.js module

# [zlib](https://bun.com/reference/node/zlib)

The `'node:zlib'` module provides compression and decompression APIs for the zlib library, including Gzip, Deflate, Brotli, and raw deflate/inflate streams.

It offers both streaming and callback-based methods, with configurable compression levels and flush modes, making it suitable for data compression, HTTP content encoding, and file archiving.

Works in Bun

Fully implemented. 98% of Node.js's test suite passes.

* ### namespace [constants](https://bun.com/reference/node/zlib/constants)

  + const [BROTLI\_DECODE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODE): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_BLOCK\_TYPE\_TREES](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_BLOCK_TYPE_TREES): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_CONTEXT\_MAP](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_CONTEXT_MAP): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_CONTEXT\_MODES](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_CONTEXT_MODES): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_RING\_BUFFER\_1](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_RING_BUFFER_1): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_RING\_BUFFER\_2](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_RING_BUFFER_2): number
  + const [BROTLI\_DECODER\_ERROR\_ALLOC\_TREE\_GROUPS](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_ALLOC_TREE_GROUPS): number
  + const [BROTLI\_DECODER\_ERROR\_DICTIONARY\_NOT\_SET](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_DICTIONARY_NOT_SET): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_BLOCK\_LENGTH\_1](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_BLOCK_LENGTH_1): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_BLOCK\_LENGTH\_2](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_BLOCK_LENGTH_2): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_CL\_SPACE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_CL_SPACE): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_CONTEXT\_MAP\_REPEAT](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_CONTEXT_MAP_REPEAT): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_DICTIONARY](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_DICTIONARY): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_DISTANCE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_DISTANCE): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_EXUBERANT\_META\_NIBBLE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_EXUBERANT_META_NIBBLE): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_EXUBERANT\_NIBBLE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_EXUBERANT_NIBBLE): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_HUFFMAN\_SPACE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_HUFFMAN_SPACE): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_PADDING\_1](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_PADDING_1): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_PADDING\_2](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_PADDING_2): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_RESERVED](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_RESERVED): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_SIMPLE\_HUFFMAN\_ALPHABET](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_SIMPLE_HUFFMAN_ALPHABET): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_SIMPLE\_HUFFMAN\_SAME](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_SIMPLE_HUFFMAN_SAME): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_TRANSFORM](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_TRANSFORM): number
  + const [BROTLI\_DECODER\_ERROR\_FORMAT\_WINDOW\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_FORMAT_WINDOW_BITS): number
  + const [BROTLI\_DECODER\_ERROR\_INVALID\_ARGUMENTS](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_INVALID_ARGUMENTS): number
  + const [BROTLI\_DECODER\_ERROR\_UNREACHABLE](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_ERROR_UNREACHABLE): number
  + const [BROTLI\_DECODER\_NEEDS\_MORE\_INPUT](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_NEEDS_MORE_INPUT): number
  + const [BROTLI\_DECODER\_NEEDS\_MORE\_OUTPUT](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_NEEDS_MORE_OUTPUT): number
  + const [BROTLI\_DECODER\_NO\_ERROR](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_NO_ERROR): number
  + const [BROTLI\_DECODER\_PARAM\_DISABLE\_RING\_BUFFER\_REALLOCATION](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_PARAM_DISABLE_RING_BUFFER_REALLOCATION): number
  + const [BROTLI\_DECODER\_PARAM\_LARGE\_WINDOW](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_PARAM_LARGE_WINDOW): number
  + const [BROTLI\_DECODER\_RESULT\_ERROR](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_RESULT_ERROR): number
  + const [BROTLI\_DECODER\_RESULT\_NEEDS\_MORE\_INPUT](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_RESULT_NEEDS_MORE_INPUT): number
  + const [BROTLI\_DECODER\_RESULT\_NEEDS\_MORE\_OUTPUT](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_RESULT_NEEDS_MORE_OUTPUT): number
  + const [BROTLI\_DECODER\_RESULT\_SUCCESS](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_RESULT_SUCCESS): number
  + const [BROTLI\_DECODER\_SUCCESS](https://bun.com/reference/node/zlib/constants/BROTLI_DECODER_SUCCESS): number
  + const [BROTLI\_DEFAULT\_MODE](https://bun.com/reference/node/zlib/constants/BROTLI_DEFAULT_MODE): number
  + const [BROTLI\_DEFAULT\_QUALITY](https://bun.com/reference/node/zlib/constants/BROTLI_DEFAULT_QUALITY): number
  + const [BROTLI\_DEFAULT\_WINDOW](https://bun.com/reference/node/zlib/constants/BROTLI_DEFAULT_WINDOW): number
  + const [BROTLI\_ENCODE](https://bun.com/reference/node/zlib/constants/BROTLI_ENCODE): number
  + const [BROTLI\_LARGE\_MAX\_WINDOW\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_LARGE_MAX_WINDOW_BITS): number
  + const [BROTLI\_MAX\_INPUT\_BLOCK\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_MAX_INPUT_BLOCK_BITS): number
  + const [BROTLI\_MAX\_QUALITY](https://bun.com/reference/node/zlib/constants/BROTLI_MAX_QUALITY): number
  + const [BROTLI\_MAX\_WINDOW\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_MAX_WINDOW_BITS): number
  + const [BROTLI\_MIN\_INPUT\_BLOCK\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_MIN_INPUT_BLOCK_BITS): number
  + const [BROTLI\_MIN\_QUALITY](https://bun.com/reference/node/zlib/constants/BROTLI_MIN_QUALITY): number
  + const [BROTLI\_MIN\_WINDOW\_BITS](https://bun.com/reference/node/zlib/constants/BROTLI_MIN_WINDOW_BITS): number
  + const [BROTLI\_MODE\_FONT](https://bun.com/reference/node/zlib/constants/BROTLI_MODE_FONT): number
  + const [BROTLI\_MODE\_GENERIC](https://bun.com/reference/node/zlib/constants/BROTLI_MODE_GENERIC): number
  + const [BROTLI\_MODE\_TEXT](https://bun.com/reference/node/zlib/constants/BROTLI_MODE_TEXT): number
  + const [BROTLI\_OPERATION\_EMIT\_METADATA](https://bun.com/reference/node/zlib/constants/BROTLI_OPERATION_EMIT_METADATA): number
  + const [BROTLI\_OPERATION\_FINISH](https://bun.com/reference/node/zlib/constants/BROTLI_OPERATION_FINISH): number
  + const [BROTLI\_OPERATION\_FLUSH](https://bun.com/reference/node/zlib/constants/BROTLI_OPERATION_FLUSH): number
  + const [BROTLI\_OPERATION\_PROCESS](https://bun.com/reference/node/zlib/constants/BROTLI_OPERATION_PROCESS): number
  + const [BROTLI\_PARAM\_DISABLE\_LITERAL\_CONTEXT\_MODELING](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_DISABLE_LITERAL_CONTEXT_MODELING): number
  + const [BROTLI\_PARAM\_LARGE\_WINDOW](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_LARGE_WINDOW): number
  + const [BROTLI\_PARAM\_LGBLOCK](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_LGBLOCK): number
  + const [BROTLI\_PARAM\_LGWIN](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_LGWIN): number
  + const [BROTLI\_PARAM\_MODE](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_MODE): number
  + const [BROTLI\_PARAM\_NDIRECT](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_NDIRECT): number
  + const [BROTLI\_PARAM\_NPOSTFIX](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_NPOSTFIX): number
  + const [BROTLI\_PARAM\_QUALITY](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_QUALITY): number
  + const [BROTLI\_PARAM\_SIZE\_HINT](https://bun.com/reference/node/zlib/constants/BROTLI_PARAM_SIZE_HINT): number
  + const [DEFLATE](https://bun.com/reference/node/zlib/constants/DEFLATE): number
  + const [DEFLATERAW](https://bun.com/reference/node/zlib/constants/DEFLATERAW): number
  + const [GUNZIP](https://bun.com/reference/node/zlib/constants/GUNZIP): number
  + const [GZIP](https://bun.com/reference/node/zlib/constants/GZIP): number
  + const [INFLATE](https://bun.com/reference/node/zlib/constants/INFLATE): number
  + const [INFLATERAW](https://bun.com/reference/node/zlib/constants/INFLATERAW): number
  + const [UNZIP](https://bun.com/reference/node/zlib/constants/UNZIP): number
  + const [Z\_BEST\_COMPRESSION](https://bun.com/reference/node/zlib/constants/Z_BEST_COMPRESSION): number
  + const [Z\_BEST\_SPEED](https://bun.com/reference/node/zlib/constants/Z_BEST_SPEED): number
  + const [Z\_BLOCK](https://bun.com/reference/node/zlib/constants/Z_BLOCK): number
  + const [Z\_BUF\_ERROR](https://bun.com/reference/node/zlib/constants/Z_BUF_ERROR): number
  + const [Z\_DATA\_ERROR](https://bun.com/reference/node/zlib/constants/Z_DATA_ERROR): number
  + const [Z\_DEFAULT\_CHUNK](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_CHUNK): number
  + const [Z\_DEFAULT\_COMPRESSION](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_COMPRESSION): number
  + const [Z\_DEFAULT\_LEVEL](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_LEVEL): number
  + const [Z\_DEFAULT\_MEMLEVEL](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_MEMLEVEL): number
  + const [Z\_DEFAULT\_STRATEGY](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_STRATEGY): number
  + const [Z\_DEFAULT\_WINDOWBITS](https://bun.com/reference/node/zlib/constants/Z_DEFAULT_WINDOWBITS): number
  + const [Z\_ERRNO](https://bun.com/reference/node/zlib/constants/Z_ERRNO): number
  + const [Z\_FILTERED](https://bun.com/reference/node/zlib/constants/Z_FILTERED): number
  + const [Z\_FINISH](https://bun.com/reference/node/zlib/constants/Z_FINISH): number
  + const [Z\_FIXED](https://bun.com/reference/node/zlib/constants/Z_FIXED): number
  + const [Z\_FULL\_FLUSH](https://bun.com/reference/node/zlib/constants/Z_FULL_FLUSH): number
  + const [Z\_HUFFMAN\_ONLY](https://bun.com/reference/node/zlib/constants/Z_HUFFMAN_ONLY): number
  + const [Z\_MAX\_CHUNK](https://bun.com/reference/node/zlib/constants/Z_MAX_CHUNK): number
  + const [Z\_MAX\_LEVEL](https://bun.com/reference/node/zlib/constants/Z_MAX_LEVEL): number
  + const [Z\_MAX\_MEMLEVEL](https://bun.com/reference/node/zlib/constants/Z_MAX_MEMLEVEL): number
  + const [Z\_MAX\_WINDOWBITS](https://bun.com/reference/node/zlib/constants/Z_MAX_WINDOWBITS): number
  + const [Z\_MEM\_ERROR](https://bun.com/reference/node/zlib/constants/Z_MEM_ERROR): number
  + const [Z\_MIN\_CHUNK](https://bun.com/reference/node/zlib/constants/Z_MIN_CHUNK): number
  + const [Z\_MIN\_LEVEL](https://bun.com/reference/node/zlib/constants/Z_MIN_LEVEL): number
  + const [Z\_MIN\_MEMLEVEL](https://bun.com/reference/node/zlib/constants/Z_MIN_MEMLEVEL): number
  + const [Z\_MIN\_WINDOWBITS](https://bun.com/reference/node/zlib/constants/Z_MIN_WINDOWBITS): number
  + const [Z\_NEED\_DICT](https://bun.com/reference/node/zlib/constants/Z_NEED_DICT): number
  + const [Z\_NO\_COMPRESSION](https://bun.com/reference/node/zlib/constants/Z_NO_COMPRESSION): number
  + const [Z\_NO\_FLUSH](https://bun.com/reference/node/zlib/constants/Z_NO_FLUSH): number
  + const [Z\_OK](https://bun.com/reference/node/zlib/constants/Z_OK): number
  + const [Z\_PARTIAL\_FLUSH](https://bun.com/reference/node/zlib/constants/Z_PARTIAL_FLUSH): number
  + const [Z\_RLE](https://bun.com/reference/node/zlib/constants/Z_RLE): number
  + const [Z\_STREAM\_END](https://bun.com/reference/node/zlib/constants/Z_STREAM_END): number
  + const [Z\_STREAM\_ERROR](https://bun.com/reference/node/zlib/constants/Z_STREAM_ERROR): number
  + const [Z\_SYNC\_FLUSH](https://bun.com/reference/node/zlib/constants/Z_SYNC_FLUSH): number
  + const [Z\_VERSION\_ERROR](https://bun.com/reference/node/zlib/constants/Z_VERSION_ERROR): number
  + const [ZLIB\_VERNUM](https://bun.com/reference/node/zlib/constants/ZLIB_VERNUM): number
  + const [ZSTD\_btlazy2](https://bun.com/reference/node/zlib/constants/ZSTD_btlazy2): number
  + const [ZSTD\_btopt](https://bun.com/reference/node/zlib/constants/ZSTD_btopt): number
  + const [ZSTD\_btultra](https://bun.com/reference/node/zlib/constants/ZSTD_btultra): number
  + const [ZSTD\_btultra2](https://bun.com/reference/node/zlib/constants/ZSTD_btultra2): number
  + const [ZSTD\_c\_chainLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_chainLog): number
  + const [ZSTD\_c\_checksumFlag](https://bun.com/reference/node/zlib/constants/ZSTD_c_checksumFlag): number
  + const [ZSTD\_c\_compressionLevel](https://bun.com/reference/node/zlib/constants/ZSTD_c_compressionLevel): number
  + const [ZSTD\_c\_contentSizeFlag](https://bun.com/reference/node/zlib/constants/ZSTD_c_contentSizeFlag): number
  + const [ZSTD\_c\_dictIDFlag](https://bun.com/reference/node/zlib/constants/ZSTD_c_dictIDFlag): number
  + const [ZSTD\_c\_enableLongDistanceMatching](https://bun.com/reference/node/zlib/constants/ZSTD_c_enableLongDistanceMatching): number
  + const [ZSTD\_c\_hashLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_hashLog): number
  + const [ZSTD\_c\_jobSize](https://bun.com/reference/node/zlib/constants/ZSTD_c_jobSize): number
  + const [ZSTD\_c\_ldmBucketSizeLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_ldmBucketSizeLog): number
  + const [ZSTD\_c\_ldmHashLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_ldmHashLog): number
  + const [ZSTD\_c\_ldmHashRateLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_ldmHashRateLog): number
  + const [ZSTD\_c\_ldmMinMatch](https://bun.com/reference/node/zlib/constants/ZSTD_c_ldmMinMatch): number
  + const [ZSTD\_c\_minMatch](https://bun.com/reference/node/zlib/constants/ZSTD_c_minMatch): number
  + const [ZSTD\_c\_nbWorkers](https://bun.com/reference/node/zlib/constants/ZSTD_c_nbWorkers): number
  + const [ZSTD\_c\_overlapLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_overlapLog): number
  + const [ZSTD\_c\_searchLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_searchLog): number
  + const [ZSTD\_c\_strategy](https://bun.com/reference/node/zlib/constants/ZSTD_c_strategy): number
  + const [ZSTD\_c\_targetLength](https://bun.com/reference/node/zlib/constants/ZSTD_c_targetLength): number
  + const [ZSTD\_c\_windowLog](https://bun.com/reference/node/zlib/constants/ZSTD_c_windowLog): number
  + const [ZSTD\_CLEVEL\_DEFAULT](https://bun.com/reference/node/zlib/constants/ZSTD_CLEVEL_DEFAULT): number
  + const [ZSTD\_COMPRESS](https://bun.com/reference/node/zlib/constants/ZSTD_COMPRESS): number
  + const [ZSTD\_d\_windowLogMax](https://bun.com/reference/node/zlib/constants/ZSTD_d_windowLogMax): number
  + const [ZSTD\_DECOMPRESS](https://bun.com/reference/node/zlib/constants/ZSTD_DECOMPRESS): number
  + const [ZSTD\_dfast](https://bun.com/reference/node/zlib/constants/ZSTD_dfast): number
  + const [ZSTD\_e\_continue](https://bun.com/reference/node/zlib/constants/ZSTD_e_continue): number
  + const [ZSTD\_e\_end](https://bun.com/reference/node/zlib/constants/ZSTD_e_end): number
  + const [ZSTD\_e\_flush](https://bun.com/reference/node/zlib/constants/ZSTD_e_flush): number
  + const [ZSTD\_error\_checksum\_wrong](https://bun.com/reference/node/zlib/constants/ZSTD_error_checksum_wrong): number
  + const [ZSTD\_error\_corruption\_detected](https://bun.com/reference/node/zlib/constants/ZSTD_error_corruption_detected): number
  + const [ZSTD\_error\_dictionary\_corrupted](https://bun.com/reference/node/zlib/constants/ZSTD_error_dictionary_corrupted): number
  + const [ZSTD\_error\_dictionary\_wrong](https://bun.com/reference/node/zlib/constants/ZSTD_error_dictionary_wrong): number
  + const [ZSTD\_error\_dictionaryCreation\_failed](https://bun.com/reference/node/zlib/constants/ZSTD_error_dictionaryCreation_failed): number
  + const [ZSTD\_error\_dstBuffer\_null](https://bun.com/reference/node/zlib/constants/ZSTD_error_dstBuffer_null): number
  + const [ZSTD\_error\_dstSize\_tooSmall](https://bun.com/reference/node/zlib/constants/ZSTD_error_dstSize_tooSmall): number
  + const [ZSTD\_error\_frameParameter\_unsupported](https://bun.com/reference/node/zlib/constants/ZSTD_error_frameParameter_unsupported): number
  + const [ZSTD\_error\_frameParameter\_windowTooLarge](https://bun.com/reference/node/zlib/constants/ZSTD_error_frameParameter_windowTooLarge): number
  + const [ZSTD\_error\_GENERIC](https://bun.com/reference/node/zlib/constants/ZSTD_error_GENERIC): number
  + const [ZSTD\_error\_init\_missing](https://bun.com/reference/node/zlib/constants/ZSTD_error_init_missing): number
  + const [ZSTD\_error\_literals\_headerWrong](https://bun.com/reference/node/zlib/constants/ZSTD_error_literals_headerWrong): number
  + const [ZSTD\_error\_maxSymbolValue\_tooLarge](https://bun.com/reference/node/zlib/constants/ZSTD_error_maxSymbolValue_tooLarge): number
  + const [ZSTD\_error\_maxSymbolValue\_tooSmall](https://bun.com/reference/node/zlib/constants/ZSTD_error_maxSymbolValue_tooSmall): number
  + const [ZSTD\_error\_memory\_allocation](https://bun.com/reference/node/zlib/constants/ZSTD_error_memory_allocation): number
  + const [ZSTD\_error\_no\_error](https://bun.com/reference/node/zlib/constants/ZSTD_error_no_error): number
  + const [ZSTD\_error\_noForwardProgress\_destFull](https://bun.com/reference/node/zlib/constants/ZSTD_error_noForwardProgress_destFull): number
  + const [ZSTD\_error\_noForwardProgress\_inputEmpty](https://bun.com/reference/node/zlib/constants/ZSTD_error_noForwardProgress_inputEmpty): number
  + const [ZSTD\_error\_parameter\_combination\_unsupported](https://bun.com/reference/node/zlib/constants/ZSTD_error_parameter_combination_unsupported): number
  + const [ZSTD\_error\_parameter\_outOfBound](https://bun.com/reference/node/zlib/constants/ZSTD_error_parameter_outOfBound): number
  + const [ZSTD\_error\_parameter\_unsupported](https://bun.com/reference/node/zlib/constants/ZSTD_error_parameter_unsupported): number
  + const [ZSTD\_error\_prefix\_unknown](https://bun.com/reference/node/zlib/constants/ZSTD_error_prefix_unknown): number
  + const [ZSTD\_error\_srcSize\_wrong](https://bun.com/reference/node/zlib/constants/ZSTD_error_srcSize_wrong): number
  + const [ZSTD\_error\_stabilityCondition\_notRespected](https://bun.com/reference/node/zlib/constants/ZSTD_error_stabilityCondition_notRespected): number
  + const [ZSTD\_error\_stage\_wrong](https://bun.com/reference/node/zlib/constants/ZSTD_error_stage_wrong): number
  + const [ZSTD\_error\_tableLog\_tooLarge](https://bun.com/reference/node/zlib/constants/ZSTD_error_tableLog_tooLarge): number
  + const [ZSTD\_error\_version\_unsupported](https://bun.com/reference/node/zlib/constants/ZSTD_error_version_unsupported): number
  + const [ZSTD\_error\_workSpace\_tooSmall](https://bun.com/reference/node/zlib/constants/ZSTD_error_workSpace_tooSmall): number
  + const [ZSTD\_fast](https://bun.com/reference/node/zlib/constants/ZSTD_fast): number
  + const [ZSTD\_greedy](https://bun.com/reference/node/zlib/constants/ZSTD_greedy): number
  + const [ZSTD\_lazy](https://bun.com/reference/node/zlib/constants/ZSTD_lazy): number
  + const [ZSTD\_lazy2](https://bun.com/reference/node/zlib/constants/ZSTD_lazy2): number
* function [brotliCompress](https://bun.com/reference/node/zlib/brotliCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [brotliCompress](https://bun.com/reference/node/zlib/brotliCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [brotliCompressSync](https://bun.com/reference/node/zlib/brotliCompressSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions)

  ): NonSharedBuffer;

  Compress a chunk of data with `BrotliCompress`.
* function [brotliDecompress](https://bun.com/reference/node/zlib/brotliDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [brotliDecompress](https://bun.com/reference/node/zlib/brotliDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [brotliDecompressSync](https://bun.com/reference/node/zlib/brotliDecompressSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `BrotliDecompress`.
* function [crc32](https://bun.com/reference/node/zlib/crc32)(

  data: string | ArrayBufferView<ArrayBufferLike>,

  value?: number

  ): number;

  Computes a 32-bit [Cyclic Redundancy Check](https://en.wikipedia.org/wiki/Cyclic_redundancy_check) checksum of `data`. If `value` is specified, it is used as the starting value of the checksum, otherwise, 0 is used as the starting value.

  @param data

  When `data` is a string, it will be encoded as UTF-8 before being used for computation.

  @param value

  An optional starting value. It must be a 32-bit unsigned integer.

  @returns

  A 32-bit unsigned integer containing the checksum.
* function [createBrotliCompress](https://bun.com/reference/node/zlib/createBrotliCompress)(

  options?: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions)

  ): [BrotliCompress](https://bun.com/reference/node/zlib/BrotliCompress);

  Creates and returns a new `BrotliCompress` object.
* function [createBrotliDecompress](https://bun.com/reference/node/zlib/createBrotliDecompress)(

  options?: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions)

  ): [BrotliDecompress](https://bun.com/reference/node/zlib/BrotliDecompress);

  Creates and returns a new `BrotliDecompress` object.
* function [createDeflate](https://bun.com/reference/node/zlib/createDeflate)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [Deflate](https://bun.com/reference/node/zlib/Deflate);

  Creates and returns a new `Deflate` object.
* function [createDeflateRaw](https://bun.com/reference/node/zlib/createDeflateRaw)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [DeflateRaw](https://bun.com/reference/node/zlib/DeflateRaw);

  Creates and returns a new `DeflateRaw` object.

  An upgrade of zlib from 1.2.8 to 1.2.11 changed behavior when `windowBits` is set to 8 for raw deflate streams. zlib would automatically set `windowBits` to 9 if was initially set to 8. Newer versions of zlib will throw an exception, so Node.js restored the original behavior of upgrading a value of 8 to 9, since passing `windowBits = 9` to zlib actually results in a compressed stream that effectively uses an 8-bit window only.
* function [createGunzip](https://bun.com/reference/node/zlib/createGunzip)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [Gunzip](https://bun.com/reference/node/zlib/Gunzip);

  Creates and returns a new `Gunzip` object.
* function [createGzip](https://bun.com/reference/node/zlib/createGzip)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [Gzip](https://bun.com/reference/node/zlib/Gzip);

  Creates and returns a new `Gzip` object. See `example`.
* function [createInflate](https://bun.com/reference/node/zlib/createInflate)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [Inflate](https://bun.com/reference/node/zlib/Inflate);

  Creates and returns a new `Inflate` object.
* function [createInflateRaw](https://bun.com/reference/node/zlib/createInflateRaw)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [InflateRaw](https://bun.com/reference/node/zlib/InflateRaw);

  Creates and returns a new `InflateRaw` object.
* function [createUnzip](https://bun.com/reference/node/zlib/createUnzip)(

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): [Unzip](https://bun.com/reference/node/zlib/Unzip);

  Creates and returns a new `Unzip` object.
* function [createZstdCompress](https://bun.com/reference/node/zlib/createZstdCompress)(

  options?: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions)

  ): [ZstdCompress](https://bun.com/reference/node/zlib/ZstdCompress);

  Creates and returns a new `ZstdCompress` object.
* function [createZstdDecompress](https://bun.com/reference/node/zlib/createZstdDecompress)(

  options?: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions)

  ): [ZstdDecompress](https://bun.com/reference/node/zlib/ZstdDecompress);

  Creates and returns a new `ZstdDecompress` object.
* function [deflate](https://bun.com/reference/node/zlib/deflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [deflate](https://bun.com/reference/node/zlib/deflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [deflateRaw](https://bun.com/reference/node/zlib/deflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [deflateRaw](https://bun.com/reference/node/zlib/deflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [deflateRawSync](https://bun.com/reference/node/zlib/deflateRawSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Compress a chunk of data with `DeflateRaw`.
* function [deflateSync](https://bun.com/reference/node/zlib/deflateSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Compress a chunk of data with `Deflate`.
* function [gunzip](https://bun.com/reference/node/zlib/gunzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [gunzip](https://bun.com/reference/node/zlib/gunzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [gunzipSync](https://bun.com/reference/node/zlib/gunzipSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `Gunzip`.
* function [gzip](https://bun.com/reference/node/zlib/gzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [gzip](https://bun.com/reference/node/zlib/gzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [gzipSync](https://bun.com/reference/node/zlib/gzipSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Compress a chunk of data with `Gzip`.
* function [inflate](https://bun.com/reference/node/zlib/inflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [inflate](https://bun.com/reference/node/zlib/inflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [inflateRaw](https://bun.com/reference/node/zlib/inflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [inflateRaw](https://bun.com/reference/node/zlib/inflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [inflateRawSync](https://bun.com/reference/node/zlib/inflateRawSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `InflateRaw`.
* function [inflateSync](https://bun.com/reference/node/zlib/inflateSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `Inflate`.
* function [unzip](https://bun.com/reference/node/zlib/unzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [unzip](https://bun.com/reference/node/zlib/unzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [unzipSync](https://bun.com/reference/node/zlib/unzipSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `Unzip`.
* function [zstdCompress](https://bun.com/reference/node/zlib/zstdCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [zstdCompress](https://bun.com/reference/node/zlib/zstdCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [zstdCompressSync](https://bun.com/reference/node/zlib/zstdCompressSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions)

  ): NonSharedBuffer;

  Compress a chunk of data with `ZstdCompress`.
* function [zstdDecompress](https://bun.com/reference/node/zlib/zstdDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [zstdDecompress](https://bun.com/reference/node/zlib/zstdDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;
* function [zstdDecompressSync](https://bun.com/reference/node/zlib/zstdDecompressSync)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options?: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions)

  ): NonSharedBuffer;

  Decompress a chunk of data with `ZstdDecompress`.

## Type definitions

* function [brotliCompress](https://bun.com/reference/node/zlib/brotliCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [brotliCompress](https://bun.com/reference/node/zlib/brotliCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [brotliCompress](https://bun.com/reference/node/zlib/brotliCompress)
* function [brotliDecompress](https://bun.com/reference/node/zlib/brotliDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [brotliDecompress](https://bun.com/reference/node/zlib/brotliDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [brotliDecompress](https://bun.com/reference/node/zlib/brotliDecompress)
* function [deflate](https://bun.com/reference/node/zlib/deflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [deflate](https://bun.com/reference/node/zlib/deflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [deflate](https://bun.com/reference/node/zlib/deflate)
* function [deflateRaw](https://bun.com/reference/node/zlib/deflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [deflateRaw](https://bun.com/reference/node/zlib/deflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [deflateRaw](https://bun.com/reference/node/zlib/deflateRaw)
* function [gunzip](https://bun.com/reference/node/zlib/gunzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [gunzip](https://bun.com/reference/node/zlib/gunzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [gunzip](https://bun.com/reference/node/zlib/gunzip)
* function [gzip](https://bun.com/reference/node/zlib/gzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [gzip](https://bun.com/reference/node/zlib/gzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [gzip](https://bun.com/reference/node/zlib/gzip)
* function [inflate](https://bun.com/reference/node/zlib/inflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [inflate](https://bun.com/reference/node/zlib/inflate)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [inflate](https://bun.com/reference/node/zlib/inflate)
* function [inflateRaw](https://bun.com/reference/node/zlib/inflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [inflateRaw](https://bun.com/reference/node/zlib/inflateRaw)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [inflateRaw](https://bun.com/reference/node/zlib/inflateRaw)
* function [unzip](https://bun.com/reference/node/zlib/unzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [unzip](https://bun.com/reference/node/zlib/unzip)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [unzip](https://bun.com/reference/node/zlib/unzip)
* function [zstdCompress](https://bun.com/reference/node/zlib/zstdCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [zstdCompress](https://bun.com/reference/node/zlib/zstdCompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [zstdCompress](https://bun.com/reference/node/zlib/zstdCompress)
* function [zstdDecompress](https://bun.com/reference/node/zlib/zstdDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  function [zstdDecompress](https://bun.com/reference/node/zlib/zstdDecompress)(

  buf: [InputType](https://bun.com/reference/node/zlib/InputType),

  options: [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions),

  callback: [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback)

  ): void;

  ### namespace [zstdDecompress](https://bun.com/reference/node/zlib/zstdDecompress)
* ### interface [BrotliCompress](https://bun.com/reference/node/zlib/BrotliCompress)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/BrotliCompress/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/BrotliCompress/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/BrotliCompress/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/BrotliCompress/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/BrotliCompress/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/BrotliCompress/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/BrotliCompress/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/BrotliCompress/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/BrotliCompress/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/BrotliCompress/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/BrotliCompress/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/BrotliCompress/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/BrotliCompress/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/BrotliCompress/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/BrotliCompress/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/BrotliCompress/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/BrotliCompress/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/BrotliCompress/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/BrotliCompress/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/BrotliCompress/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/BrotliCompress/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/BrotliCompress/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/BrotliCompress/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/BrotliCompress/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/BrotliCompress/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/BrotliCompress/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/BrotliCompress/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/BrotliCompress/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/BrotliCompress/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/BrotliCompress/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/BrotliCompress/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/BrotliCompress/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/BrotliCompress/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/BrotliCompress/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/BrotliCompress/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliCompress/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/BrotliCompress/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/BrotliCompress/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/BrotliCompress/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/BrotliCompress/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/BrotliCompress/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/BrotliCompress/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliCompress/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/BrotliCompress/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/BrotliCompress/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/BrotliCompress/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/BrotliCompress/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/BrotliCompress/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/BrotliCompress/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/BrotliCompress/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/BrotliCompress/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/BrotliCompress/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/BrotliCompress/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/BrotliCompress/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/BrotliCompress/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/BrotliCompress/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/BrotliCompress/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/BrotliCompress/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/BrotliCompress/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/BrotliCompress/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/BrotliCompress/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/BrotliCompress/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliCompress/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliCompress/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/BrotliCompress/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/BrotliCompress/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliCompress/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliCompress/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/BrotliCompress/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/BrotliCompress/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/BrotliCompress/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/BrotliCompress/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/BrotliCompress/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/BrotliCompress/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliCompress/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/BrotliCompress/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/BrotliCompress/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/BrotliCompress/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/BrotliCompress/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/BrotliCompress/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/BrotliCompress/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/BrotliCompress/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/BrotliCompress/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/BrotliCompress/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/BrotliCompress/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/BrotliCompress/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/BrotliCompress/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/BrotliCompress/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [BrotliDecompress](https://bun.com/reference/node/zlib/BrotliDecompress)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/BrotliDecompress/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/BrotliDecompress/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/BrotliDecompress/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/BrotliDecompress/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/BrotliDecompress/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/BrotliDecompress/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/BrotliDecompress/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/BrotliDecompress/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/BrotliDecompress/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/BrotliDecompress/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/BrotliDecompress/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/BrotliDecompress/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/BrotliDecompress/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/BrotliDecompress/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/BrotliDecompress/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/BrotliDecompress/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/BrotliDecompress/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/BrotliDecompress/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/BrotliDecompress/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/BrotliDecompress/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/BrotliDecompress/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/BrotliDecompress/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/BrotliDecompress/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/BrotliDecompress/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/BrotliDecompress/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/BrotliDecompress/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/BrotliDecompress/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/BrotliDecompress/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/BrotliDecompress/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/BrotliDecompress/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/BrotliDecompress/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/BrotliDecompress/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/BrotliDecompress/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/BrotliDecompress/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/BrotliDecompress/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/BrotliDecompress/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/BrotliDecompress/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/BrotliDecompress/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/BrotliDecompress/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/BrotliDecompress/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/BrotliDecompress/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/BrotliDecompress/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/BrotliDecompress/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/BrotliDecompress/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/BrotliDecompress/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/BrotliDecompress/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/BrotliDecompress/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/BrotliDecompress/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/BrotliDecompress/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/BrotliDecompress/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/BrotliDecompress/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/BrotliDecompress/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/BrotliDecompress/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/BrotliDecompress/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/BrotliDecompress/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/BrotliDecompress/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/BrotliDecompress/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/BrotliDecompress/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/BrotliDecompress/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/BrotliDecompress/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/BrotliDecompress/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/BrotliDecompress/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/BrotliDecompress/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/BrotliDecompress/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/BrotliDecompress/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/BrotliDecompress/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/BrotliDecompress/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/BrotliDecompress/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/BrotliDecompress/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/BrotliDecompress/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/BrotliDecompress/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/BrotliDecompress/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/BrotliDecompress/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/BrotliDecompress/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/BrotliDecompress/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/BrotliDecompress/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/BrotliDecompress/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/BrotliDecompress/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/BrotliDecompress/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/BrotliDecompress/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/BrotliDecompress/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/BrotliDecompress/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/BrotliDecompress/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/BrotliDecompress/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/BrotliDecompress/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/BrotliDecompress/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/BrotliDecompress/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [BrotliOptions](https://bun.com/reference/node/zlib/BrotliOptions)

  + [chunkSize](https://bun.com/reference/node/zlib/BrotliOptions/chunkSize)?: number
  + [finishFlush](https://bun.com/reference/node/zlib/BrotliOptions/finishFlush)?: number
  + [flush](https://bun.com/reference/node/zlib/BrotliOptions/flush)?: number
  + [info](https://bun.com/reference/node/zlib/BrotliOptions/info)?: boolean

    If `true`, returns an object with `buffer` and `engine`.
  + [maxOutputLength](https://bun.com/reference/node/zlib/BrotliOptions/maxOutputLength)?: number

    Limits output size when using [convenience methods](https://nodejs.org/docs/latest-v24.x/api/zlib.html#convenience-methods).
  + [params](https://bun.com/reference/node/zlib/BrotliOptions/params)?: { 

    \_\_index[

    key: number

    ]: number | boolean;

    Each key is a `constants.BROTLI_*` constant.

     }
* ### interface [Deflate](https://bun.com/reference/node/zlib/Deflate)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/Deflate/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Deflate/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/Deflate/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/Deflate/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/Deflate/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/Deflate/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/Deflate/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/Deflate/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/Deflate/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/Deflate/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/Deflate/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/Deflate/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/Deflate/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/Deflate/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/Deflate/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/Deflate/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/Deflate/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/Deflate/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/Deflate/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/Deflate/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/Deflate/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/Deflate/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/Deflate/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/Deflate/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/Deflate/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/Deflate/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/Deflate/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/Deflate/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/Deflate/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/Deflate/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/Deflate/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/Deflate/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/Deflate/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/Deflate/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/Deflate/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Deflate/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/Deflate/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/Deflate/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/Deflate/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/Deflate/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/Deflate/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/Deflate/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Deflate/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/Deflate/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/Deflate/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/Deflate/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/Deflate/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/Deflate/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/Deflate/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/Deflate/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/Deflate/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/Deflate/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/Deflate/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Deflate/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/Deflate/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/Deflate/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/Deflate/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/Deflate/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/Deflate/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/Deflate/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/Deflate/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/Deflate/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Deflate/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Deflate/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [params](https://bun.com/reference/node/zlib/Deflate/params)(

    level: number,

    strategy: number,

    callback: () => void

    ): void;
  + [pause](https://bun.com/reference/node/zlib/Deflate/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/Deflate/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Deflate/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Deflate/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/Deflate/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/Deflate/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/Deflate/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/Deflate/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/Deflate/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/Deflate/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Deflate/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [reset](https://bun.com/reference/node/zlib/Deflate/reset)(): void;
  + [resume](https://bun.com/reference/node/zlib/Deflate/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/Deflate/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/Deflate/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/Deflate/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/Deflate/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/Deflate/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/Deflate/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/Deflate/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/Deflate/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/Deflate/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/Deflate/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/Deflate/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/Deflate/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [DeflateRaw](https://bun.com/reference/node/zlib/DeflateRaw)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/DeflateRaw/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/DeflateRaw/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/DeflateRaw/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/DeflateRaw/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/DeflateRaw/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/DeflateRaw/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/DeflateRaw/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/DeflateRaw/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/DeflateRaw/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/DeflateRaw/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/DeflateRaw/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/DeflateRaw/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/DeflateRaw/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/DeflateRaw/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/DeflateRaw/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/DeflateRaw/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/DeflateRaw/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/DeflateRaw/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/DeflateRaw/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/DeflateRaw/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/DeflateRaw/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/DeflateRaw/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/DeflateRaw/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/DeflateRaw/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/DeflateRaw/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/DeflateRaw/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/DeflateRaw/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/DeflateRaw/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/DeflateRaw/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/DeflateRaw/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/DeflateRaw/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/DeflateRaw/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/DeflateRaw/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/DeflateRaw/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/DeflateRaw/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/DeflateRaw/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/DeflateRaw/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/DeflateRaw/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/DeflateRaw/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/DeflateRaw/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/DeflateRaw/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/DeflateRaw/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/DeflateRaw/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/DeflateRaw/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/DeflateRaw/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/DeflateRaw/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/DeflateRaw/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/DeflateRaw/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/DeflateRaw/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/DeflateRaw/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/DeflateRaw/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/DeflateRaw/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/DeflateRaw/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/DeflateRaw/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/DeflateRaw/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/DeflateRaw/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/DeflateRaw/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/DeflateRaw/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/DeflateRaw/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/DeflateRaw/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/DeflateRaw/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/DeflateRaw/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/DeflateRaw/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/DeflateRaw/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [params](https://bun.com/reference/node/zlib/DeflateRaw/params)(

    level: number,

    strategy: number,

    callback: () => void

    ): void;
  + [pause](https://bun.com/reference/node/zlib/DeflateRaw/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/DeflateRaw/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/DeflateRaw/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/DeflateRaw/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/DeflateRaw/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/DeflateRaw/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/DeflateRaw/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/DeflateRaw/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/DeflateRaw/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/DeflateRaw/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/DeflateRaw/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [reset](https://bun.com/reference/node/zlib/DeflateRaw/reset)(): void;
  + [resume](https://bun.com/reference/node/zlib/DeflateRaw/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/DeflateRaw/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/DeflateRaw/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/DeflateRaw/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/DeflateRaw/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/DeflateRaw/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/DeflateRaw/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/DeflateRaw/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/DeflateRaw/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/DeflateRaw/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/DeflateRaw/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/DeflateRaw/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/DeflateRaw/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [Gunzip](https://bun.com/reference/node/zlib/Gunzip)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/Gunzip/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Gunzip/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/Gunzip/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/Gunzip/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/Gunzip/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/Gunzip/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/Gunzip/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/Gunzip/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/Gunzip/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/Gunzip/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/Gunzip/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/Gunzip/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/Gunzip/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/Gunzip/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/Gunzip/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/Gunzip/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/Gunzip/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/Gunzip/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/Gunzip/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/Gunzip/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/Gunzip/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/Gunzip/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/Gunzip/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/Gunzip/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/Gunzip/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/Gunzip/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/Gunzip/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/Gunzip/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/Gunzip/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/Gunzip/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/Gunzip/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/Gunzip/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/Gunzip/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/Gunzip/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/Gunzip/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gunzip/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/Gunzip/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/Gunzip/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/Gunzip/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/Gunzip/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/Gunzip/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/Gunzip/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gunzip/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/Gunzip/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/Gunzip/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/Gunzip/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/Gunzip/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/Gunzip/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/Gunzip/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/Gunzip/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/Gunzip/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/Gunzip/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/Gunzip/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Gunzip/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/Gunzip/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/Gunzip/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/Gunzip/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/Gunzip/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/Gunzip/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/Gunzip/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/Gunzip/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/Gunzip/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gunzip/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gunzip/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/Gunzip/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/Gunzip/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gunzip/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gunzip/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/Gunzip/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/Gunzip/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/Gunzip/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/Gunzip/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/Gunzip/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/Gunzip/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gunzip/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/Gunzip/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/Gunzip/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/Gunzip/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/Gunzip/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/Gunzip/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/Gunzip/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/Gunzip/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/Gunzip/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/Gunzip/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/Gunzip/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/Gunzip/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/Gunzip/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/Gunzip/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [Gzip](https://bun.com/reference/node/zlib/Gzip)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/Gzip/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Gzip/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/Gzip/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/Gzip/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/Gzip/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/Gzip/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/Gzip/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/Gzip/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/Gzip/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/Gzip/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/Gzip/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/Gzip/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/Gzip/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/Gzip/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/Gzip/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/Gzip/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/Gzip/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/Gzip/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/Gzip/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/Gzip/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/Gzip/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/Gzip/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/Gzip/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/Gzip/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/Gzip/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/Gzip/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/Gzip/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/Gzip/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/Gzip/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/Gzip/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/Gzip/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/Gzip/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/Gzip/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/Gzip/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/Gzip/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Gzip/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/Gzip/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/Gzip/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/Gzip/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/Gzip/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/Gzip/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/Gzip/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Gzip/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/Gzip/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/Gzip/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/Gzip/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/Gzip/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/Gzip/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/Gzip/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/Gzip/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/Gzip/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/Gzip/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/Gzip/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Gzip/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/Gzip/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/Gzip/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/Gzip/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/Gzip/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/Gzip/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/Gzip/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/Gzip/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/Gzip/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Gzip/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Gzip/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/Gzip/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/Gzip/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Gzip/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Gzip/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/Gzip/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/Gzip/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/Gzip/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/Gzip/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/Gzip/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/Gzip/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Gzip/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/Gzip/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/Gzip/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/Gzip/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/Gzip/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/Gzip/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/Gzip/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/Gzip/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/Gzip/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/Gzip/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/Gzip/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/Gzip/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/Gzip/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/Gzip/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [Inflate](https://bun.com/reference/node/zlib/Inflate)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/Inflate/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Inflate/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/Inflate/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/Inflate/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/Inflate/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/Inflate/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/Inflate/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/Inflate/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/Inflate/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/Inflate/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/Inflate/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/Inflate/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/Inflate/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/Inflate/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/Inflate/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/Inflate/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/Inflate/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/Inflate/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/Inflate/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/Inflate/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/Inflate/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/Inflate/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/Inflate/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/Inflate/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/Inflate/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/Inflate/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/Inflate/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/Inflate/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/Inflate/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/Inflate/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/Inflate/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/Inflate/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/Inflate/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/Inflate/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/Inflate/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Inflate/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/Inflate/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/Inflate/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/Inflate/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/Inflate/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/Inflate/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/Inflate/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Inflate/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/Inflate/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/Inflate/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/Inflate/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/Inflate/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/Inflate/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/Inflate/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/Inflate/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/Inflate/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/Inflate/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/Inflate/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Inflate/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/Inflate/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/Inflate/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/Inflate/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/Inflate/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/Inflate/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/Inflate/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/Inflate/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/Inflate/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Inflate/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Inflate/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/Inflate/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/Inflate/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Inflate/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Inflate/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/Inflate/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/Inflate/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/Inflate/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/Inflate/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/Inflate/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/Inflate/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Inflate/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [reset](https://bun.com/reference/node/zlib/Inflate/reset)(): void;
  + [resume](https://bun.com/reference/node/zlib/Inflate/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/Inflate/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/Inflate/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/Inflate/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/Inflate/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/Inflate/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/Inflate/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/Inflate/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/Inflate/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/Inflate/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/Inflate/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/Inflate/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/Inflate/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [InflateRaw](https://bun.com/reference/node/zlib/InflateRaw)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/InflateRaw/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/InflateRaw/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/InflateRaw/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/InflateRaw/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/InflateRaw/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/InflateRaw/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/InflateRaw/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/InflateRaw/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/InflateRaw/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/InflateRaw/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/InflateRaw/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/InflateRaw/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/InflateRaw/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/InflateRaw/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/InflateRaw/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/InflateRaw/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/InflateRaw/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/InflateRaw/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/InflateRaw/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/InflateRaw/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/InflateRaw/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/InflateRaw/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/InflateRaw/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/InflateRaw/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/InflateRaw/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/InflateRaw/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/InflateRaw/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/InflateRaw/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/InflateRaw/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/InflateRaw/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/InflateRaw/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/InflateRaw/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/InflateRaw/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/InflateRaw/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/InflateRaw/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/InflateRaw/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/InflateRaw/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/InflateRaw/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/InflateRaw/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/InflateRaw/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/InflateRaw/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/InflateRaw/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/InflateRaw/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/InflateRaw/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/InflateRaw/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/InflateRaw/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/InflateRaw/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/InflateRaw/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/InflateRaw/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/InflateRaw/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/InflateRaw/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/InflateRaw/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/InflateRaw/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/InflateRaw/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/InflateRaw/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/InflateRaw/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/InflateRaw/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/InflateRaw/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/InflateRaw/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/InflateRaw/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/InflateRaw/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/InflateRaw/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/InflateRaw/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/InflateRaw/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/InflateRaw/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/InflateRaw/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/InflateRaw/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/InflateRaw/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/InflateRaw/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/InflateRaw/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/InflateRaw/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/InflateRaw/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/InflateRaw/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/InflateRaw/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/InflateRaw/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [reset](https://bun.com/reference/node/zlib/InflateRaw/reset)(): void;
  + [resume](https://bun.com/reference/node/zlib/InflateRaw/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/InflateRaw/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/InflateRaw/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/InflateRaw/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/InflateRaw/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/InflateRaw/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/InflateRaw/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/InflateRaw/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/InflateRaw/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/InflateRaw/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/InflateRaw/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/InflateRaw/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/InflateRaw/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [Unzip](https://bun.com/reference/node/zlib/Unzip)

  Transform streams are `Duplex` streams where the output is in some way related to the input. Like all `Duplex` streams, `Transform` streams implement both the `Readable` and `Writable` interfaces.

  Examples of `Transform` streams include:

  + `zlib streams`
  + `crypto streams`

  + [allowHalfOpen](https://bun.com/reference/node/zlib/Unzip/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Unzip/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/Unzip/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/Unzip/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/Unzip/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/Unzip/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/Unzip/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/Unzip/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/Unzip/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/Unzip/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/Unzip/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/Unzip/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/Unzip/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/Unzip/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/Unzip/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/Unzip/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/Unzip/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/Unzip/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/Unzip/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/Unzip/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/Unzip/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/Unzip/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/Unzip/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/Unzip/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/Unzip/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/Unzip/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/Unzip/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/Unzip/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/Unzip/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/Unzip/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/Unzip/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/Unzip/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/Unzip/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/Unzip/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/Unzip/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/Unzip/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/Unzip/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/Unzip/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/Unzip/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/Unzip/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/Unzip/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/Unzip/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/Unzip/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/Unzip/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/Unzip/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/Unzip/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/Unzip/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/Unzip/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/Unzip/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/Unzip/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/Unzip/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/Unzip/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/Unzip/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Unzip/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/Unzip/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/Unzip/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/Unzip/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/Unzip/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/Unzip/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/Unzip/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/Unzip/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/Unzip/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/Unzip/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/Unzip/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/Unzip/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/Unzip/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/Unzip/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/Unzip/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/Unzip/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/Unzip/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/Unzip/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/Unzip/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/Unzip/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/Unzip/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/Unzip/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/Unzip/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/Unzip/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/Unzip/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/Unzip/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/Unzip/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/Unzip/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/Unzip/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/Unzip/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/Unzip/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/Unzip/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/Unzip/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/Unzip/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/Unzip/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [Zlib](https://bun.com/reference/node/zlib/Zlib)

  + readonly [bytesWritten](https://bun.com/reference/node/zlib/Zlib/bytesWritten): number
  + [shell](https://bun.com/reference/node/zlib/Zlib/shell)?: string | boolean
  + [close](https://bun.com/reference/node/zlib/Zlib/close)(

    callback?: () => void

    ): void;
  + [flush](https://bun.com/reference/node/zlib/Zlib/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/Zlib/flush)(

    callback?: () => void

    ): void;
* ### interface [ZlibOptions](https://bun.com/reference/node/zlib/ZlibOptions)

  + [chunkSize](https://bun.com/reference/node/zlib/ZlibOptions/chunkSize)?: number
  + [dictionary](https://bun.com/reference/node/zlib/ZlibOptions/dictionary)?: [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | ArrayBufferView<ArrayBufferLike>
  + [finishFlush](https://bun.com/reference/node/zlib/ZlibOptions/finishFlush)?: number
  + [flush](https://bun.com/reference/node/zlib/ZlibOptions/flush)?: number
  + [info](https://bun.com/reference/node/zlib/ZlibOptions/info)?: boolean

    If `true`, returns an object with `buffer` and `engine`.
  + [level](https://bun.com/reference/node/zlib/ZlibOptions/level)?: number
  + [maxOutputLength](https://bun.com/reference/node/zlib/ZlibOptions/maxOutputLength)?: number

    Limits output size when using convenience methods.
  + [memLevel](https://bun.com/reference/node/zlib/ZlibOptions/memLevel)?: number
  + [strategy](https://bun.com/reference/node/zlib/ZlibOptions/strategy)?: number
  + [windowBits](https://bun.com/reference/node/zlib/ZlibOptions/windowBits)?: number
* ### interface [ZlibParams](https://bun.com/reference/node/zlib/ZlibParams)

  + [params](https://bun.com/reference/node/zlib/ZlibParams/params)(

    level: number,

    strategy: number,

    callback: () => void

    ): void;
* ### interface [ZlibReset](https://bun.com/reference/node/zlib/ZlibReset)

  + [reset](https://bun.com/reference/node/zlib/ZlibReset/reset)(): void;
* ### interface [ZstdCompress](https://bun.com/reference/node/zlib/ZstdCompress)

  + [allowHalfOpen](https://bun.com/reference/node/zlib/ZstdCompress/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/ZstdCompress/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/ZstdCompress/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/ZstdCompress/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/ZstdCompress/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/ZstdCompress/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/ZstdCompress/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/ZstdCompress/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/ZstdCompress/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/ZstdCompress/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/ZstdCompress/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/ZstdCompress/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/ZstdCompress/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/ZstdCompress/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/ZstdCompress/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/ZstdCompress/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/ZstdCompress/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/ZstdCompress/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/ZstdCompress/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/ZstdCompress/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/ZstdCompress/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/ZstdCompress/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/ZstdCompress/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/ZstdCompress/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/ZstdCompress/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/ZstdCompress/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/ZstdCompress/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/ZstdCompress/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/ZstdCompress/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/ZstdCompress/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/ZstdCompress/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/ZstdCompress/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/ZstdCompress/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/ZstdCompress/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/ZstdCompress/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdCompress/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/ZstdCompress/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/ZstdCompress/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/ZstdCompress/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/ZstdCompress/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/ZstdCompress/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/ZstdCompress/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdCompress/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/ZstdCompress/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/ZstdCompress/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/ZstdCompress/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/ZstdCompress/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/ZstdCompress/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/ZstdCompress/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/ZstdCompress/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/ZstdCompress/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/ZstdCompress/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/ZstdCompress/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/ZstdCompress/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/ZstdCompress/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/ZstdCompress/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/ZstdCompress/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/ZstdCompress/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/ZstdCompress/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/ZstdCompress/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/ZstdCompress/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/ZstdCompress/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdCompress/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdCompress/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/ZstdCompress/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/ZstdCompress/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdCompress/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdCompress/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/ZstdCompress/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/ZstdCompress/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/ZstdCompress/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/ZstdCompress/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/ZstdCompress/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/ZstdCompress/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdCompress/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/ZstdCompress/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/ZstdCompress/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/ZstdCompress/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/ZstdCompress/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/ZstdCompress/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/ZstdCompress/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/ZstdCompress/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/ZstdCompress/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/ZstdCompress/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/ZstdCompress/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/ZstdCompress/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/ZstdCompress/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/ZstdCompress/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [ZstdDecompress](https://bun.com/reference/node/zlib/ZstdDecompress)

  + [allowHalfOpen](https://bun.com/reference/node/zlib/ZstdDecompress/allowHalfOpen): boolean

    If `false` then the stream will automatically end the writable side when the readable side ends. Set initially by the `allowHalfOpen` constructor option, which defaults to `true`.

    This can be changed manually to change the half-open behavior of an existing `Duplex` stream instance, but must be changed before the `'end'` event is emitted.
  + readonly [bytesWritten](https://bun.com/reference/node/zlib/ZstdDecompress/bytesWritten): number
  + readonly [closed](https://bun.com/reference/node/zlib/ZstdDecompress/closed): boolean

    Is `true` after `'close'` has been emitted.
  + [destroyed](https://bun.com/reference/node/zlib/ZstdDecompress/destroyed): boolean

    Is `true` after `readable.destroy()` has been called.
  + readonly [errored](https://bun.com/reference/node/zlib/ZstdDecompress/errored): null | [Error](https://bun.com/reference/globals/Error)

    Returns error if the stream has been destroyed with an error.
  + [readable](https://bun.com/reference/node/zlib/ZstdDecompress/readable): boolean

    Is `true` if it is safe to call read, which means the stream has not been destroyed or emitted `'error'` or `'end'`.
  + readonly [readableAborted](https://bun.com/reference/node/zlib/ZstdDecompress/readableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'end'`.
  + readonly [readableDidRead](https://bun.com/reference/node/zlib/ZstdDecompress/readableDidRead): boolean

    Returns whether `'data'` has been emitted.
  + readonly [readableEncoding](https://bun.com/reference/node/zlib/ZstdDecompress/readableEncoding): null | BufferEncoding

    Getter for the property `encoding` of a given `Readable` stream. The `encoding` property can be set using the setEncoding method.
  + readonly [readableEnded](https://bun.com/reference/node/zlib/ZstdDecompress/readableEnded): boolean

    Becomes `true` when [`'end'`](https://nodejs.org/docs/latest-v24.x/api/stream.html#event-end) event is emitted.
  + readonly [readableFlowing](https://bun.com/reference/node/zlib/ZstdDecompress/readableFlowing): null | boolean

    This property reflects the current state of a `Readable` stream as described in the [Three states](https://nodejs.org/docs/latest-v24.x/api/stream.html#three-states) section.
  + readonly [readableHighWaterMark](https://bun.com/reference/node/zlib/ZstdDecompress/readableHighWaterMark): number

    Returns the value of `highWaterMark` passed when creating this `Readable`.
  + readonly [readableLength](https://bun.com/reference/node/zlib/ZstdDecompress/readableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be read. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [readableObjectMode](https://bun.com/reference/node/zlib/ZstdDecompress/readableObjectMode): boolean

    Getter for the property `objectMode` of a given `Readable` stream.
  + [shell](https://bun.com/reference/node/zlib/ZstdDecompress/shell)?: string | boolean
  + readonly [writable](https://bun.com/reference/node/zlib/ZstdDecompress/writable): boolean

    Is `true` if it is safe to call `writable.write()`, which means the stream has not been destroyed, errored, or ended.
  + readonly [writableAborted](https://bun.com/reference/node/zlib/ZstdDecompress/writableAborted): boolean

    Returns whether the stream was destroyed or errored before emitting `'finish'`.
  + readonly [writableCorked](https://bun.com/reference/node/zlib/ZstdDecompress/writableCorked): number

    Number of times `writable.uncork()` needs to be called in order to fully uncork the stream.
  + readonly [writableEnded](https://bun.com/reference/node/zlib/ZstdDecompress/writableEnded): boolean

    Is `true` after `writable.end()` has been called. This property does not indicate whether the data has been flushed, for this use `writable.writableFinished` instead.
  + readonly [writableFinished](https://bun.com/reference/node/zlib/ZstdDecompress/writableFinished): boolean

    Is set to `true` immediately before the `'finish'` event is emitted.
  + readonly [writableHighWaterMark](https://bun.com/reference/node/zlib/ZstdDecompress/writableHighWaterMark): number

    Return the value of `highWaterMark` passed when creating this `Writable`.
  + readonly [writableLength](https://bun.com/reference/node/zlib/ZstdDecompress/writableLength): number

    This property contains the number of bytes (or objects) in the queue ready to be written. The value provides introspection data regarding the status of the `highWaterMark`.
  + readonly [writableNeedDrain](https://bun.com/reference/node/zlib/ZstdDecompress/writableNeedDrain): boolean

    Is `true` if the stream's buffer has been full and stream will emit `'drain'`.
  + readonly [writableObjectMode](https://bun.com/reference/node/zlib/ZstdDecompress/writableObjectMode): boolean

    Getter for the property `objectMode` of a given `Writable` stream.
  + [\_construct](https://bun.com/reference/node/zlib/ZstdDecompress/_construct)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_destroy](https://bun.com/reference/node/zlib/ZstdDecompress/_destroy)(

    error: null | [Error](https://bun.com/reference/globals/Error),

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_final](https://bun.com/reference/node/zlib/ZstdDecompress/_final)(

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_flush](https://bun.com/reference/node/zlib/ZstdDecompress/_flush)(

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_read](https://bun.com/reference/node/zlib/ZstdDecompress/_read)(

    size: number

    ): void;
  + [\_transform](https://bun.com/reference/node/zlib/ZstdDecompress/_transform)(

    chunk: any,

    encoding: BufferEncoding,

    callback: [TransformCallback](https://bun.com/reference/node/stream/default/TransformCallback)

    ): void;
  + [\_write](https://bun.com/reference/node/zlib/ZstdDecompress/_write)(

    chunk: any,

    encoding: BufferEncoding,

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [\_writev](https://bun.com/reference/node/zlib/ZstdDecompress/_writev)(

    chunks: { chunk: any; encoding: BufferEncoding }[],

    callback: (error?: null | [Error](https://bun.com/reference/globals/Error)) => void

    ): void;
  + [[Symbol.asyncDispose]](https://bun.com/reference/node/zlib/ZstdDecompress/[asyncDispose])(): Promise<void>;

    Calls `readable.destroy()` with an `AbortError` and returns a promise that fulfills when the stream is finished.
  + [[Symbol.asyncIterator]](https://bun.com/reference/node/zlib/ZstdDecompress/[asyncIterator])(): AsyncIterator<any>;

    @returns

    `AsyncIterator` to fully consume the stream.
  + [[events.captureRejectionSymbol]](https://bun.com/reference/node/zlib/ZstdDecompress/[captureRejectionSymbol])<K>(

    error: [Error](https://bun.com/reference/globals/Error),

    event: string | symbol,

    ...args: AnyRest

    ): void;
  + [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'close',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'drain',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'end',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'finish',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'pause',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'readable',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'resume',

    listener: () => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe

    [addListener](https://bun.com/reference/node/zlib/ZstdDecompress/addListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Event emitter The defined events on documents including:

    1. close
    2. data
    3. drain
    4. end
    5. error
    6. finish
    7. pause
    8. pipe
    9. readable
    10. resume
    11. unpipe
  + [asIndexedPairs](https://bun.com/reference/node/zlib/ZstdDecompress/asIndexedPairs)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with chunks of the underlying stream paired with a counter in the form `[index, chunk]`. The first index value is `0` and it increases by 1 for each chunk produced.

    @returns

    a stream of indexed pairs.
  + [close](https://bun.com/reference/node/zlib/ZstdDecompress/close)(

    callback?: () => void

    ): void;
  + [compose](https://bun.com/reference/node/zlib/ZstdDecompress/compose)<T extends ReadableStream>(

    stream: ComposeFnParam | T | Iterable<T, any, any> | AsyncIterable<T, any, any>,

    options?: { signal: [AbortSignal](https://bun.com/reference/globals/AbortSignal) }

    ): T;
  + [cork](https://bun.com/reference/node/zlib/ZstdDecompress/cork)(): void;

    The `writable.cork()` method forces all written data to be buffered in memory. The buffered data will be flushed when either the uncork or end methods are called.

    The primary intent of `writable.cork()` is to accommodate a situation in which several small chunks are written to the stream in rapid succession. Instead of immediately forwarding them to the underlying destination, `writable.cork()` buffers all the chunks until `writable.uncork()` is called, which will pass them all to `writable._writev()`, if present. This prevents a head-of-line blocking situation where data is being buffered while waiting for the first small chunk to be processed. However, use of `writable.cork()` without implementing `writable._writev()` may have an adverse effect on throughput.

    See also: `writable.uncork()`, `writable._writev()`.
  + [destroy](https://bun.com/reference/node/zlib/ZstdDecompress/destroy)(

    error?: [Error](https://bun.com/reference/globals/Error)

    ): this;

    Destroy the stream. Optionally emit an `'error'` event, and emit a `'close'` event (unless `emitClose` is set to `false`). After this call, the readable stream will release any internal resources and subsequent calls to `push()` will be ignored.

    Once `destroy()` has been called any further calls will be a no-op and no further errors except from `_destroy()` may be emitted as `'error'`.

    Implementors should not override this method, but instead implement `readable._destroy()`.

    @param error

    Error which will be passed as payload in `'error'` event
  + [drop](https://bun.com/reference/node/zlib/ZstdDecompress/drop)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks dropped from the start.

    @param limit

    the number of chunks to drop from the readable.

    @returns

    a stream with *limit* chunks dropped from the start.
  + [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'close'

    ): boolean;

    Synchronously calls each of the listeners registered for the event named `eventName`, in the order they were registered, passing the supplied arguments to each.

    Returns `true` if the event had listeners, `false` otherwise.

    ```
    import { EventEmitter } from 'node:events';
    const myEmitter = new EventEmitter();

    // First listener
    myEmitter.on('event', function firstListener() {
      console.log('Helloooo! first listener');
    });
    // Second listener
    myEmitter.on('event', function secondListener(arg1, arg2) {
      console.log(`event with parameters ${arg1}, ${arg2} in second listener`);
    });
    // Third listener
    myEmitter.on('event', function thirdListener(...args) {
      const parameters = args.join(', ');
      console.log(`event with parameters ${parameters} in third listener`);
    });

    console.log(myEmitter.listeners('event'));

    myEmitter.emit('event', 1, 2, 3, 4, 5);

    // Prints:
    // [
    //   [Function: firstListener],
    //   [Function: secondListener],
    //   [Function: thirdListener]
    // ]
    // Helloooo! first listener
    // event with parameters 1, 2 in second listener
    // event with parameters 1, 2, 3, 4, 5 in third listener
    ```

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'data',

    chunk: any

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'drain'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'end'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'error',

    err: [Error](https://bun.com/reference/globals/Error)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'finish'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'pause'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'pipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'readable'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'resume'

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: 'unpipe',

    src: [Readable](https://bun.com/reference/node/stream/default/Readable)

    ): boolean;

    [emit](https://bun.com/reference/node/zlib/ZstdDecompress/emit)(

    event: string | symbol,

    ...args: any[]

    ): boolean;
  + [end](https://bun.com/reference/node/zlib/ZstdDecompress/end)(

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    [end](https://bun.com/reference/node/zlib/ZstdDecompress/end)(

    chunk: any,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    [end](https://bun.com/reference/node/zlib/ZstdDecompress/end)(

    chunk: any,

    encoding: BufferEncoding,

    cb?: () => void

    ): this;

    Calling the `writable.end()` method signals that no more data will be written to the `Writable`. The optional `chunk` and `encoding` arguments allow one final additional chunk of data to be written immediately before closing the stream.

    Calling the write method after calling end will raise an error.

    ```
    // Write 'hello, ' and then end with 'world!'.
    import fs from 'node:fs';
    const file = fs.createWriteStream('example.txt');
    file.write('hello, ');
    file.end('world!');
    // Writing more now is not allowed!
    ```

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding if `chunk` is a string
  + [eventNames](https://bun.com/reference/node/zlib/ZstdDecompress/eventNames)(): string | symbol[];

    Returns an array listing the events for which the emitter has registered listeners. The values in the array are strings or `Symbol`s.

    ```
    import { EventEmitter } from 'node:events';

    const myEE = new EventEmitter();
    myEE.on('foo', () => {});
    myEE.on('bar', () => {});

    const sym = Symbol('symbol');
    myEE.on(sym, () => {});

    console.log(myEE.eventNames());
    // Prints: [ 'foo', 'bar', Symbol(symbol) ]
    ```
  + [every](https://bun.com/reference/node/zlib/ZstdDecompress/every)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.every` and calls *fn* on each chunk in the stream to check if all awaited return values are truthy value for *fn*. Once an *fn* call on a chunk `await`ed return value is falsy, the stream is destroyed and the promise is fulfilled with `false`. If all of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `true`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for every one of the chunks.
  + [filter](https://bun.com/reference/node/zlib/ZstdDecompress/filter)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows filtering the stream. For each chunk in the stream the *fn* function will be called and if it returns a truthy value, the chunk will be passed to the result stream. If the *fn* function returns a promise - that promise will be `await`ed.

    @param fn

    a function to filter chunks from the stream. Async or not.

    @returns

    a stream filtered with the predicate *fn*.
  + [find](https://bun.com/reference/node/zlib/ZstdDecompress/find)<T>(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => data is T,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<undefined | T>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.

    [find](https://bun.com/reference/node/zlib/ZstdDecompress/find)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<any>;

    This method is similar to `Array.prototype.find` and calls *fn* on each chunk in the stream to find a chunk with a truthy value for *fn*. Once an *fn* call's awaited return value is truthy, the stream is destroyed and the promise is fulfilled with value for which *fn* returned a truthy value. If all of the *fn* calls on the chunks return a falsy value, the promise is fulfilled with `undefined`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to the first chunk for which *fn* evaluated with a truthy value, or `undefined` if no element was found.
  + [flatMap](https://bun.com/reference/node/zlib/ZstdDecompress/flatMap)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream by applying the given callback to each chunk of the stream and then flattening the result.

    It is possible to return a stream or another iterable or async iterable from *fn* and the result streams will be merged (flattened) into the returned stream.

    @param fn

    a function to map over every chunk in the stream. May be async. May be a stream or generator.

    @returns

    a stream flat-mapped with the function *fn*.
  + [flush](https://bun.com/reference/node/zlib/ZstdDecompress/flush)(

    kind?: number,

    callback?: () => void

    ): void;

    [flush](https://bun.com/reference/node/zlib/ZstdDecompress/flush)(

    callback?: () => void

    ): void;
  + [forEach](https://bun.com/reference/node/zlib/ZstdDecompress/forEach)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => void | Promise<void>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<void>;

    This method allows iterating a stream. For each chunk in the stream the *fn* function will be called. If the *fn* function returns a promise - that promise will be `await`ed.

    This method is different from `for await...of` loops in that it can optionally process chunks concurrently. In addition, a `forEach` iteration can only be stopped by having passed a `signal` option and aborting the related AbortController while `for await...of` can be stopped with `break` or `return`. In either case the stream will be destroyed.

    This method is different from listening to the `'data'` event in that it uses the `readable` event in the underlying machinary and can limit the number of concurrent *fn* calls.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise for when the stream has finished.
  + [getMaxListeners](https://bun.com/reference/node/zlib/ZstdDecompress/getMaxListeners)(): number;

    Returns the current max listener value for the `EventEmitter` which is either set by `emitter.setMaxListeners(n)` or defaults to EventEmitter.defaultMaxListeners.
  + [isPaused](https://bun.com/reference/node/zlib/ZstdDecompress/isPaused)(): boolean;

    The `readable.isPaused()` method returns the current operating state of the `Readable`. This is used primarily by the mechanism that underlies the `readable.pipe()` method. In most typical cases, there will be no reason to use this method directly.

    ```
    const readable = new stream.Readable();

    readable.isPaused(); // === false
    readable.pause();
    readable.isPaused(); // === true
    readable.resume();
    readable.isPaused(); // === false
    ```
  + [iterator](https://bun.com/reference/node/zlib/ZstdDecompress/iterator)(

    options?: { destroyOnReturn: boolean }

    ): AsyncIterator<any>;

    The iterator created by this method gives users the option to cancel the destruction of the stream if the `for await...of` loop is exited by `return`, `break`, or `throw`, or if the iterator should destroy the stream if the stream emitted an error during iteration.
  + [listenerCount](https://bun.com/reference/node/zlib/ZstdDecompress/listenerCount)<K>(

    eventName: string | symbol,

    listener?: Function

    ): number;

    Returns the number of listeners listening for the event named `eventName`. If `listener` is provided, it will return how many times the listener is found in the list of the listeners of the event.

    @param eventName

    The name of the event being listened for

    @param listener

    The event handler function
  + [listeners](https://bun.com/reference/node/zlib/ZstdDecompress/listeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    console.log(util.inspect(server.listeners('connection')));
    // Prints: [ [Function] ]
    ```
  + [map](https://bun.com/reference/node/zlib/ZstdDecompress/map)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => any,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method allows mapping over the stream. The *fn* function will be called for every chunk in the stream. If the *fn* function returns a promise - that promise will be `await`ed before being passed to the result stream.

    @param fn

    a function to map over every chunk in the stream. Async or not.

    @returns

    a stream mapped with the function *fn*.
  + [off](https://bun.com/reference/node/zlib/ZstdDecompress/off)<K>(

    eventName: string | symbol,

    listener: (...args: any[]) => void

    ): this;

    Alias for `emitter.removeListener()`.
  + [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the end of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.on('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.on('foo', () => console.log('a'));
    myEE.prependListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'drain',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'end',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'finish',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'pause',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'readable',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'resume',

    listener: () => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [on](https://bun.com/reference/node/zlib/ZstdDecompress/on)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time** `listener` function for the event named `eventName`. The next time `eventName` is triggered, this listener is removed and then invoked.

    ```
    server.once('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    By default, event listeners are invoked in the order they are added. The `emitter.prependOnceListener()` method can be used as an alternative to add the event listener to the beginning of the listeners array.

    ```
    import { EventEmitter } from 'node:events';
    const myEE = new EventEmitter();
    myEE.once('foo', () => console.log('a'));
    myEE.prependOnceListener('foo', () => console.log('b'));
    myEE.emit('foo');
    // Prints:
    //   b
    //   a
    ```

    @param listener

    The callback function

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'drain',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'end',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'finish',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'pause',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'readable',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'resume',

    listener: () => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [once](https://bun.com/reference/node/zlib/ZstdDecompress/once)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [pause](https://bun.com/reference/node/zlib/ZstdDecompress/pause)(): this;

    The `readable.pause()` method will cause a stream in flowing mode to stop emitting `'data'` events, switching out of flowing mode. Any data that becomes available will remain in the internal buffer.

    ```
    const readable = getReadableStreamSomehow();
    readable.on('data', (chunk) => {
      console.log(`Received ${chunk.length} bytes of data.`);
      readable.pause();
      console.log('There will be no additional data for 1 second.');
      setTimeout(() => {
        console.log('Now data will start flowing again.');
        readable.resume();
      }, 1000);
    });
    ```

    The `readable.pause()` method has no effect if there is a `'readable'` event listener.
  + [pipe](https://bun.com/reference/node/zlib/ZstdDecompress/pipe)<T extends WritableStream>(

    destination: T,

    options?: { end: boolean }

    ): T;
  + [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds the `listener` function to the *beginning* of the listeners array for the event named `eventName`. No checks are made to see if the `listener` has already been added. Multiple calls passing the same combination of `eventName` and `listener` will result in the `listener` being added, and called, multiple times.

    ```
    server.prependListener('connection', (stream) => {
      console.log('someone connected!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'close',

    listener: () => void

    ): this;

    Adds a **one-time**`listener` function for the event named `eventName` to the *beginning* of the listeners array. The next time `eventName` is triggered, this listener is removed, and then invoked.

    ```
    server.prependOnceListener('connection', (stream) => {
      console.log('Ah, we have our first user!');
    });
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    @param listener

    The callback function

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'end',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [prependOnceListener](https://bun.com/reference/node/zlib/ZstdDecompress/prependOnceListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [push](https://bun.com/reference/node/zlib/ZstdDecompress/push)(

    chunk: any,

    encoding?: BufferEncoding

    ): boolean;
  + [rawListeners](https://bun.com/reference/node/zlib/ZstdDecompress/rawListeners)<K>(

    eventName: string | symbol

    ): Function[];

    Returns a copy of the array of listeners for the event named `eventName`, including any wrappers (such as those created by `.once()`).

    ```
    import { EventEmitter } from 'node:events';
    const emitter = new EventEmitter();
    emitter.once('log', () => console.log('log once'));

    // Returns a new Array with a function `onceWrapper` which has a property
    // `listener` which contains the original listener bound above
    const listeners = emitter.rawListeners('log');
    const logFnWrapper = listeners[0];

    // Logs "log once" to the console and does not unbind the `once` event
    logFnWrapper.listener();

    // Logs "log once" to the console and removes the listener
    logFnWrapper();

    emitter.on('log', () => console.log('log persistently'));
    // Will return a new Array with a single function bound by `.on()` above
    const newListeners = emitter.rawListeners('log');

    // Logs "log persistently" twice
    newListeners[0]();
    emitter.emit('log');
    ```
  + [read](https://bun.com/reference/node/zlib/ZstdDecompress/read)(

    size?: number

    ): any;

    The `readable.read()` method reads data out of the internal buffer and returns it. If no data is available to be read, `null` is returned. By default, the data is returned as a `Buffer` object unless an encoding has been specified using the `readable.setEncoding()` method or the stream is operating in object mode.

    The optional `size` argument specifies a specific number of bytes to read. If `size` bytes are not available to be read, `null` will be returned *unless* the stream has ended, in which case all of the data remaining in the internal buffer will be returned.

    If the `size` argument is not specified, all of the data contained in the internal buffer will be returned.

    The `size` argument must be less than or equal to 1 GiB.

    The `readable.read()` method should only be called on `Readable` streams operating in paused mode. In flowing mode, `readable.read()` is called automatically until the internal buffer is fully drained.

    ```
    const readable = getReadableStreamSomehow();

    // 'readable' may be triggered multiple times as data is buffered in
    readable.on('readable', () => {
      let chunk;
      console.log('Stream is readable (new data received in buffer)');
      // Use a loop to make sure we read all currently available data
      while (null !== (chunk = readable.read())) {
        console.log(`Read ${chunk.length} bytes of data...`);
      }
    });

    // 'end' will be triggered once when there is no more data available
    readable.on('end', () => {
      console.log('Reached end of stream.');
    });
    ```

    Each call to `readable.read()` returns a chunk of data, or `null`. The chunks are not concatenated. A `while` loop is necessary to consume all data currently in the buffer. When reading a large file `.read()` may return `null`, having consumed all buffered content so far, but there is still more data to come not yet buffered. In this case a new `'readable'` event will be emitted when there is more data in the buffer. Finally the `'end'` event will be emitted when there is no more data to come.

    Therefore to read a file's whole contents from a `readable`, it is necessary to collect chunks across multiple `'readable'` events:

    ```
    const chunks = [];

    readable.on('readable', () => {
      let chunk;
      while (null !== (chunk = readable.read())) {
        chunks.push(chunk);
      }
    });

    readable.on('end', () => {
      const content = chunks.join('');
    });
    ```

    A `Readable` stream in object mode will always return a single item from a call to `readable.read(size)`, regardless of the value of the `size` argument.

    If the `readable.read()` method returns a chunk of data, a `'data'` event will also be emitted.

    Calling read after the `'end'` event has been emitted will return `null`. No runtime error will be raised.

    @param size

    Optional argument to specify how much data to read.
  + [reduce](https://bun.com/reference/node/zlib/ZstdDecompress/reduce)<T = any>(

    fn: (previous: any, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial?: undefined,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.

    [reduce](https://bun.com/reference/node/zlib/ZstdDecompress/reduce)<T = any>(

    fn: (previous: T, data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => T,

    initial: T,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<T>;

    This method calls *fn* on each chunk of the stream in order, passing it the result from the calculation on the previous element. It returns a promise for the final value of the reduction.

    If no *initial* value is supplied the first chunk of the stream is used as the initial value. If the stream is empty, the promise is rejected with a `TypeError` with the `ERR_INVALID_ARGS` code property.

    The reducer function iterates the stream element-by-element which means that there is no *concurrency* parameter or parallelism. To perform a reduce concurrently, you can extract the async function to `readable.map` method.

    @param fn

    a reducer function to call over every chunk in the stream. Async or not.

    @param initial

    the initial value to use in the reduction.

    @returns

    a promise for the final value of the reduction.
  + [removeAllListeners](https://bun.com/reference/node/zlib/ZstdDecompress/removeAllListeners)(

    eventName?: string | symbol

    ): this;

    Removes all listeners, or those of the specified `eventName`.

    It is bad practice to remove listeners added elsewhere in the code, particularly when the `EventEmitter` instance was created by some other component or module (e.g. sockets or file streams).

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'close',

    listener: () => void

    ): this;

    Removes the specified `listener` from the listener array for the event named `eventName`.

    ```
    const callback = (stream) => {
      console.log('someone connected!');
    };
    server.on('connection', callback);
    // ...
    server.removeListener('connection', callback);
    ```

    `removeListener()` will remove, at most, one instance of a listener from the listener array. If any single listener has been added multiple times to the listener array for the specified `eventName`, then `removeListener()` must be called multiple times to remove each instance.

    Once an event is emitted, all listeners attached to it at the time of emitting are called in order. This implies that any `removeListener()` or `removeAllListeners()` calls *after* emitting and *before* the last listener finishes execution will not remove them from`emit()` in progress. Subsequent events behave as expected.

    ```
    import { EventEmitter } from 'node:events';
    class MyEmitter extends EventEmitter {}
    const myEmitter = new MyEmitter();

    const callbackA = () => {
      console.log('A');
      myEmitter.removeListener('event', callbackB);
    };

    const callbackB = () => {
      console.log('B');
    };

    myEmitter.on('event', callbackA);

    myEmitter.on('event', callbackB);

    // callbackA removes listener callbackB but it will still be called.
    // Internal listener array at time of emit [callbackA, callbackB]
    myEmitter.emit('event');
    // Prints:
    //   A
    //   B

    // callbackB is now removed.
    // Internal listener array [callbackA]
    myEmitter.emit('event');
    // Prints:
    //   A
    ```

    Because listeners are managed using an internal array, calling this will change the position indices of any listener registered *after* the listener being removed. This will not impact the order in which listeners are called, but it means that any copies of the listener array as returned by the `emitter.listeners()` method will need to be recreated.

    When a single function has been added as a handler multiple times for a single event (as in the example below), `removeListener()` will remove the most recently added instance. In the example the `once('ping')` listener is removed:

    ```
    import { EventEmitter } from 'node:events';
    const ee = new EventEmitter();

    function pong() {
      console.log('pong');
    }

    ee.on('ping', pong);
    ee.once('ping', pong);
    ee.removeListener('ping', pong);

    ee.emit('ping');
    ee.emit('ping');
    ```

    Returns a reference to the `EventEmitter`, so that calls can be chained.

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'data',

    listener: (chunk: any) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'drain',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'end',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'error',

    listener: (err: [Error](https://bun.com/reference/globals/Error)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'finish',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'pause',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'pipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'readable',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'resume',

    listener: () => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: 'unpipe',

    listener: (src: [Readable](https://bun.com/reference/node/stream/default/Readable)) => void

    ): this;

    [removeListener](https://bun.com/reference/node/zlib/ZstdDecompress/removeListener)(

    event: string | symbol,

    listener: (...args: any[]) => void

    ): this;
  + [resume](https://bun.com/reference/node/zlib/ZstdDecompress/resume)(): this;

    The `readable.resume()` method causes an explicitly paused `Readable` stream to resume emitting `'data'` events, switching the stream into flowing mode.

    The `readable.resume()` method can be used to fully consume the data from a stream without actually processing any of that data:

    ```
    getReadableStreamSomehow()
      .resume()
      .on('end', () => {
        console.log('Reached the end, but did not read anything.');
      });
    ```

    The `readable.resume()` method has no effect if there is a `'readable'` event listener.
  + [setDefaultEncoding](https://bun.com/reference/node/zlib/ZstdDecompress/setDefaultEncoding)(

    encoding: BufferEncoding

    ): this;

    The `writable.setDefaultEncoding()` method sets the default `encoding` for a `Writable` stream.

    @param encoding

    The new default encoding
  + [setEncoding](https://bun.com/reference/node/zlib/ZstdDecompress/setEncoding)(

    encoding: BufferEncoding

    ): this;

    The `readable.setEncoding()` method sets the character encoding for data read from the `Readable` stream.

    By default, no encoding is assigned and stream data will be returned as `Buffer` objects. Setting an encoding causes the stream data to be returned as strings of the specified encoding rather than as `Buffer` objects. For instance, calling `readable.setEncoding('utf8')` will cause the output data to be interpreted as UTF-8 data, and passed as strings. Calling `readable.setEncoding('hex')` will cause the data to be encoded in hexadecimal string format.

    The `Readable` stream will properly handle multi-byte characters delivered through the stream that would otherwise become improperly decoded if simply pulled from the stream as `Buffer` objects.

    ```
    const readable = getReadableStreamSomehow();
    readable.setEncoding('utf8');
    readable.on('data', (chunk) => {
      assert.equal(typeof chunk, 'string');
      console.log('Got %d characters of string data:', chunk.length);
    });
    ```

    @param encoding

    The encoding to use.
  + [setMaxListeners](https://bun.com/reference/node/zlib/ZstdDecompress/setMaxListeners)(

    n: number

    ): this;

    By default `EventEmitter`s will print a warning if more than `10` listeners are added for a particular event. This is a useful default that helps finding memory leaks. The `emitter.setMaxListeners()` method allows the limit to be modified for this specific `EventEmitter` instance. The value can be set to `Infinity` (or `0`) to indicate an unlimited number of listeners.

    Returns a reference to the `EventEmitter`, so that calls can be chained.
  + [some](https://bun.com/reference/node/zlib/ZstdDecompress/some)(

    fn: (data: any, options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>) => boolean | Promise<boolean>,

    options?: [ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions)

    ): Promise<boolean>;

    This method is similar to `Array.prototype.some` and calls *fn* on each chunk in the stream until the awaited return value is `true` (or any truthy value). Once an *fn* call on a chunk `await`ed return value is truthy, the stream is destroyed and the promise is fulfilled with `true`. If none of the *fn* calls on the chunks return a truthy value, the promise is fulfilled with `false`.

    @param fn

    a function to call on each chunk of the stream. Async or not.

    @returns

    a promise evaluating to `true` if *fn* returned a truthy value for at least one of the chunks.
  + [take](https://bun.com/reference/node/zlib/ZstdDecompress/take)(

    limit: number,

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): [Readable](https://bun.com/reference/node/stream/default/Readable);

    This method returns a new stream with the first *limit* chunks.

    @param limit

    the number of chunks to take from the readable.

    @returns

    a stream with *limit* chunks taken.
  + [toArray](https://bun.com/reference/node/zlib/ZstdDecompress/toArray)(

    options?: Pick<[ArrayOptions](https://bun.com/reference/node/stream/default/ArrayOptions), 'signal'>

    ): Promise<any[]>;

    This method allows easily obtaining the contents of a stream.

    As this method reads the entire stream into memory, it negates the benefits of streams. It's intended for interoperability and convenience, not as the primary way to consume streams.

    @returns

    a promise containing an array with the contents of the stream.
  + [uncork](https://bun.com/reference/node/zlib/ZstdDecompress/uncork)(): void;

    The `writable.uncork()` method flushes all data buffered since cork was called.

    When using `writable.cork()` and `writable.uncork()` to manage the buffering of writes to a stream, defer calls to `writable.uncork()` using `process.nextTick()`. Doing so allows batching of all `writable.write()` calls that occur within a given Node.js event loop phase.

    ```
    stream.cork();
    stream.write('some ');
    stream.write('data ');
    process.nextTick(() => stream.uncork());
    ```

    If the `writable.cork()` method is called multiple times on a stream, the same number of calls to `writable.uncork()` must be called to flush the buffered data.

    ```
    stream.cork();
    stream.write('some ');
    stream.cork();
    stream.write('data ');
    process.nextTick(() => {
      stream.uncork();
      // The data will not be flushed until uncork() is called a second time.
      stream.uncork();
    });
    ```

    See also: `writable.cork()`.
  + [unpipe](https://bun.com/reference/node/zlib/ZstdDecompress/unpipe)(

    destination?: WritableStream

    ): this;

    The `readable.unpipe()` method detaches a `Writable` stream previously attached using the pipe method.

    If the `destination` is not specified, then *all* pipes are detached.

    If the `destination` is specified, but no pipe is set up for it, then the method does nothing.

    ```
    import fs from 'node:fs';
    const readable = getReadableStreamSomehow();
    const writable = fs.createWriteStream('file.txt');
    // All the data from readable goes into 'file.txt',
    // but only for the first second.
    readable.pipe(writable);
    setTimeout(() => {
      console.log('Stop writing to file.txt.');
      readable.unpipe(writable);
      console.log('Manually close the file stream.');
      writable.end();
    }, 1000);
    ```

    @param destination

    Optional specific stream to unpipe
  + [unshift](https://bun.com/reference/node/zlib/ZstdDecompress/unshift)(

    chunk: any,

    encoding?: BufferEncoding

    ): void;

    Passing `chunk` as `null` signals the end of the stream (EOF) and behaves the same as `readable.push(null)`, after which no more data can be written. The EOF signal is put at the end of the buffer and any buffered data will still be flushed.

    The `readable.unshift()` method pushes a chunk of data back into the internal buffer. This is useful in certain situations where a stream is being consumed by code that needs to "un-consume" some amount of data that it has optimistically pulled out of the source, so that the data can be passed on to some other party.

    The `stream.unshift(chunk)` method cannot be called after the `'end'` event has been emitted or a runtime error will be thrown.

    Developers using `stream.unshift()` often should consider switching to use of a `Transform` stream instead. See the `API for stream implementers` section for more information.

    ```
    // Pull off a header delimited by \n\n.
    // Use unshift() if we get too much.
    // Call the callback with (error, header, stream).
    import { StringDecoder } from 'node:string_decoder';
    function parseHeader(stream, callback) {
      stream.on('error', callback);
      stream.on('readable', onReadable);
      const decoder = new StringDecoder('utf8');
      let header = '';
      function onReadable() {
        let chunk;
        while (null !== (chunk = stream.read())) {
          const str = decoder.write(chunk);
          if (str.includes('\n\n')) {
            // Found the header boundary.
            const split = str.split(/\n\n/);
            header += split.shift();
            const remaining = split.join('\n\n');
            const buf = Buffer.from(remaining, 'utf8');
            stream.removeListener('error', callback);
            // Remove the 'readable' listener before unshifting.
            stream.removeListener('readable', onReadable);
            if (buf.length)
              stream.unshift(buf);
            // Now the body of the message can be read from the stream.
            callback(null, header, stream);
            return;
          }
          // Still reading the header.
          header += str;
        }
      }
    }
    ```

    Unlike push, `stream.unshift(chunk)` will not end the reading process by resetting the internal reading state of the stream. This can cause unexpected results if `readable.unshift()` is called during a read (i.e. from within a \_read implementation on a custom stream). Following the call to `readable.unshift()` with an immediate push will reset the reading state appropriately, however it is best to simply avoid calling `readable.unshift()` while in the process of performing a read.

    @param chunk

    Chunk of data to unshift onto the read queue. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray}, {DataView} or `null`. For object mode streams, `chunk` may be any JavaScript value.

    @param encoding

    Encoding of string chunks. Must be a valid `Buffer` encoding, such as `'utf8'` or `'ascii'`.
  + [wrap](https://bun.com/reference/node/zlib/ZstdDecompress/wrap)(

    stream: ReadableStream

    ): this;

    Prior to Node.js 0.10, streams did not implement the entire `node:stream` module API as it is currently defined. (See `Compatibility` for more information.)

    When using an older Node.js library that emits `'data'` events and has a pause method that is advisory only, the `readable.wrap()` method can be used to create a `Readable` stream that uses the old stream as its data source.

    It will rarely be necessary to use `readable.wrap()` but the method has been provided as a convenience for interacting with older Node.js applications and libraries.

    ```
    import { OldReader } from './old-api-module.js';
    import { Readable } from 'node:stream';
    const oreader = new OldReader();
    const myReader = new Readable().wrap(oreader);

    myReader.on('readable', () => {
      myReader.read(); // etc.
    });
    ```

    @param stream

    An "old style" readable stream
  + [write](https://bun.com/reference/node/zlib/ZstdDecompress/write)(

    chunk: any,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.

    [write](https://bun.com/reference/node/zlib/ZstdDecompress/write)(

    chunk: any,

    encoding: BufferEncoding,

    callback?: (error: undefined | null | [Error](https://bun.com/reference/globals/Error)) => void

    ): boolean;

    The `writable.write()` method writes some data to the stream, and calls the supplied `callback` once the data has been fully handled. If an error occurs, the `callback` will be called with the error as its first argument. The `callback` is called asynchronously and before `'error'` is emitted.

    The return value is `true` if the internal buffer is less than the `highWaterMark` configured when the stream was created after admitting `chunk`. If `false` is returned, further attempts to write data to the stream should stop until the `'drain'` event is emitted.

    While a stream is not draining, calls to `write()` will buffer `chunk`, and return false. Once all currently buffered chunks are drained (accepted for delivery by the operating system), the `'drain'` event will be emitted. Once `write()` returns false, do not write more chunks until the `'drain'` event is emitted. While calling `write()` on a stream that is not draining is allowed, Node.js will buffer all written chunks until maximum memory usage occurs, at which point it will abort unconditionally. Even before it aborts, high memory usage will cause poor garbage collector performance and high RSS (which is not typically released back to the system, even after the memory is no longer required). Since TCP sockets may never drain if the remote peer does not read the data, writing a socket that is not draining may lead to a remotely exploitable vulnerability.

    Writing data while the stream is not draining is particularly problematic for a `Transform`, because the `Transform` streams are paused by default until they are piped or a `'data'` or `'readable'` event handler is added.

    If the data to be written can be generated or fetched on demand, it is recommended to encapsulate the logic into a `Readable` and use pipe. However, if calling `write()` is preferred, it is possible to respect backpressure and avoid memory issues using the `'drain'` event:

    ```
    function write(data, cb) {
      if (!stream.write(data)) {
        stream.once('drain', cb);
      } else {
        process.nextTick(cb);
      }
    }

    // Wait for cb to be called before doing any other write.
    write('hello', () => {
      console.log('Write completed, do more writes now.');
    });
    ```

    A `Writable` stream in object mode will always ignore the `encoding` argument.

    @param chunk

    Optional data to write. For streams not operating in object mode, `chunk` must be a {string}, {Buffer}, {TypedArray} or {DataView}. For object mode streams, `chunk` may be any JavaScript value other than `null`.

    @param encoding

    The encoding, if `chunk` is a string.

    @param callback

    Callback for when this chunk of data is flushed.

    @returns

    `false` if the stream wishes for the calling code to wait for the `'drain'` event to be emitted before continuing to write additional data; otherwise `true`.
* ### interface [ZstdOptions](https://bun.com/reference/node/zlib/ZstdOptions)

  + [chunkSize](https://bun.com/reference/node/zlib/ZstdOptions/chunkSize)?: number
  + [dictionary](https://bun.com/reference/node/zlib/ZstdOptions/dictionary)?: ArrayBufferView<ArrayBufferLike>

    Optional dictionary used to improve compression efficiency when compressing or decompressing data that shares common patterns with the dictionary.
  + [finishFlush](https://bun.com/reference/node/zlib/ZstdOptions/finishFlush)?: number
  + [flush](https://bun.com/reference/node/zlib/ZstdOptions/flush)?: number
  + [info](https://bun.com/reference/node/zlib/ZstdOptions/info)?: boolean

    If `true`, returns an object with `buffer` and `engine`.
  + [maxOutputLength](https://bun.com/reference/node/zlib/ZstdOptions/maxOutputLength)?: number

    Limits output size when using [convenience methods](https://nodejs.org/docs/latest-v24.x/api/zlib.html#convenience-methods).
  + [params](https://bun.com/reference/node/zlib/ZstdOptions/params)?: { 

    \_\_index[

    key: number

    ]: number | boolean;

     }

    Key-value object containing indexed [Zstd parameters](https://nodejs.org/docs/latest-v24.x/api/zlib.html#zstd-constants).
* type [CompressCallback](https://bun.com/reference/node/zlib/CompressCallback) = (error: [Error](https://bun.com/reference/globals/Error) | null, result: NonSharedBuffer) => void
* type [InputType](https://bun.com/reference/node/zlib/InputType) = string | [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | NodeJS.ArrayBufferView