# Clojure\(Script\) Cheat Sheet

#### Map items in a vector to a vector of keyed maps

```text
(def days-of-week
  ["Monday" "Tuesday" "Wednesday" "Thursday" "Friday" "Saturday" "Weekdays" "Weekends"])

(def dow-vec
  (into [] (map #(hash-map :dow_name %) days-of-week)))
```

#### Target first and last children with Stylefy modes

Useful for grids and forms

```text
(defn elem
  [children]
  [:div (s/use-style {::s/mode {:first-child {:margin-top "-0.5em"}
                                :last-child  {:margin-bottom "0.5em"}}})
   children])
```

#### Create uniquely-keyed items with a random UUID

Used when Reagent complains about how each element should have a unique key.

```text
(defn create-uuid
  []
  (keyword (str (random-uuid))))

(def itms ["Foo" "Bar" "Baz"])

(defn render-itm
  [itm]
  ^{:key (create-uuid)}
  [:span itm])
  
(defn render-itms
  []
  (doall (map render-itm itms)))
```

#### Dangerously set raw HTML string as page content \(nothing user-generated!\)

[https://github.com/reagent-project/reagent/issues/14\#issuecomment-34156523](https://github.com/reagent-project/reagent/issues/14#issuecomment-34156523)

```text
(defn dangerous-html
  ([component content]
   (dangerous-html component nil content))
  ([component props content]
   [component (assoc props :dangerouslySetInnerHTML {:__html content})]))
   
(dangerous-html :div "<i>italics</i>")
```

#### Cancel an event

```text
(defn cancel-evt [evt]
  (.preventDefault evt)
  (.stopPropagation evt))
```

#### Canonical way to get a value from a React event \(reagent\)

```text
(defn evt->val [evt]
  (oget evt "target.value"))
```

#### Strip a set of characters from a string

Stolen from [https://www.rosettacode.org/wiki/Strip\_a\_set\_of\_characters\_from\_a\_string\#Clojure](https://www.rosettacode.org/wiki/Strip_a_set_of_characters_from_a_string#Clojure)

```text
(defn strip-chars [s to-strip]
  (apply str (remove #((set to-strip) %) s)))
```

#### Round a float to 2 decimal points

```text
(ns my-ns
  (:require
   [goog.string :as googstring]
   [goog.string.format]))
 
(defn decimal-round [f]
  (googstring/format "%.2f" f))
```



