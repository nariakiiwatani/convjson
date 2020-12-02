# convjson

C++ header-only library for converting JSON programmatically.

```
	using namespace convjson::helpers;
	nlohmann::json data = {
		{"key1", {{"arr1", 1},{"arr2", 2}}},
		{"key2", {"arr3", 3}},
	};
	
	Value(data)
	.castTo<Object>()
	.modify(CherryPick({"key2"}))
	.effect(Print())
	.effect(Save("obj"))
	.effect(SaveObjEach("obj_"))
	.convert(Dispatch(2,
		[](std::size_t index, const nlohmann::json &src) {
			return nlohmann::json{{"wrap_"+std::to_string(index), src}};
		}))
	.effect(Save("array"))
	.effect(SaveArrayEach("array_"))
	.convert(ToObj([](std::size_t index, const nlohmann::json &item, const nlohmann::json &src) {
		return make_pair("item_"+std::to_string(index), item);
	}))
	.effect(Print())
	;
```