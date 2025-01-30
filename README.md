Updates to the original self-RAG
- transform_query:
    - Multiple queries instead of one query
    - Generate queries based on context (useful docs)
        - Important for allowing HKG->BKK to be answered
    - Add hypothesis as a consideration for new queries, so that generic insights can be generated from documents that might not be immediately useful for the current question (e.g. draw inference about configuration vs crew seats based on doc for other airplane type)
        - Important for allowing B-LBI crew seats to be answered
    - Generic prompt engineering
- grade_documents:
    - Append useful docs, instead of overwrite
    - Retain history of graded documents, to skip evaluating those graded before among the newly retrieved docs
    - Relax the grading by taking vs_queries into account, beyond just the immediate question
        - Important for allowing B-LBI crew seats to be answered 
- retrieve:
    - Given multiple queries are issued to retrieve docs, apply deduplication in response
    - Allow the use of semantic_hybrid as search_type by removing `@search.captions` from response
- others:
    - Fix the infinite loop for grade_generation_v_documents_and_question, in which "not supported" will lead to re-generating the same answer with available docs, without looking for additional information 

To-do
- evaluate Q one by one
    - optimized for vectorstore retrieval
    - useful
    - not repeated
- distill useful info from docs