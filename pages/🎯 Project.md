-
- query-sort-by:: status
  query-sort-desc:: true
  query-properties:: [:page :status :area :topic]
  #+BEGIN_QUERY
  {:title [:div.font-bold "All projects list"]
   :query [:find (pull ?p [*])
   :where
    [?p :block/name ?title]
    (not [(= ?title "template")])
    [?p :block/properties ?props]
    [(get ?props :type) ?type]
    [(= ?type #{"🎯 Project"})]
   ]}
  #+END_QUERY
-
- query-table:: false
  #+BEGIN_QUERY
  {:title [:div.font-bold "Active projects tasks"]
   :query [:find (pull ?b [*])
   :where
    [?b :block/page ?p]
    [?p :block/properties ?props]
    [(get ?props :type) ?type]
    [(= ?type #{"🎯 Project"})]
    [(get ?props :status) ?status]
    [(= ?status #{"⏺ inprogress"})]
    (task ?b #{"LATER" "NOW"}) ]}
  #+END_QUERY
-