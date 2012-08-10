# Introduction
This is a small JavaScript project that will allow you to create dependencies of options between two HTML select elements. When the value of the first select changes, it automatically fills the new options of the second with results of an Ajax request.

# Requeriments
* MooTools 1.1

# Usage
```javascript
new SelectDependency(target, source, options);
```

### Quick example
```javascript
new SelectDependency('city', 'country', {
	
	url: 'index.php',
	
	requestValueKey: 'country_id',
	requestParams: {
		controller: 'ajax',
		task:       'getCities'
	},
	
	responseLabelKey: 'name',
	responseValueKey: 'id'

});
```

### Parameters
* target: The target select element where to push new values after the Ajax request.
* source: The source select element which triggers the update of the values of the target element when its value is changed
* options: An object containing any of the following:
	* onChange
	* method
	* url
	* requestValueKey
	* requestParams
	* responseLabelKey
	* responseValueKey
	* responseSelectedKey
	* loadingText

# Options
<table>
	<tr>
		<th>Optiona Name</th>
		<th>Default Value</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>onChange</td>
		<td>*Empty (Class.empty)*</td>
		<td>This Event gets fired every time the options of the target element has been populated.</td>
	</tr>
	<tr>
		<td>url</td>
		<td></td>
		<td>Base URL for the Ajax Request.</td>
	</tr>
	<tr>
		<td>requestValueKey</td>
		<td>value</td>
		<td>Name of the parameter containing the current value of the source element to be sent with the Ajax Request.</td>
	</tr>
	<tr>
		<td>requestParams</td>
		<td>{}</td>
		<td>Map of additional parameters to send with the Ajax Request.</td>
	</tr>
	<tr>
		<td>responseLabelKey</td>
		<td>label</td>
		<td>Name of the parameter containing the label of the response.</td>
	</tr>
	<tr>
		<td>responseValueKey</td>
		<td>value</td>
		<td>Name of the parameter containing the value of the response.</td>
	</tr>
	<tr>
		<td>responseSelectedKey</td>
		<td>selected</td>
		<td>Name of the parameter from the response indicating the option selected by default.</td>
	</tr>
	<tr>
		<td>loadingText</td>
		<td>Loading...</td>
		<td>Use this to translate or change the loading text</td>
	</tr>
</table>

# Example

The following example shows how to update a list of cities for a previously selected country.

When the user selects a country, an Ajax is sent to the server and the list of cities gets automatically updated with a new list of cities from the server response.

### HTML Code
```html
<select name="country_id" id="country_id">
	<option value="33">Argentina</option>
	<option value="24">Australia</option>
	<option value="15">Austria</option>
	<option value="55">Azerbaijan</option>
	<option value="10">Belgium</option>
	<option value="27">Brazil</option>
	<option value="57">Cambodia</option>
	<option value="26">Canada</option>
	<option value="59">China</option>
	<option value="37">Costa Rica</option>
	<option value="18">Croatia</option>
	<option value="52">Cuba</option>
	<option value="20">Cyprus</option>
	<option value="5">Czech Republic</option>
	<option value="14">Denmark</option>
	<option value="2">France</option>
	<option value="9">Germany</option>
	<option value="8">Greece</option>
	<option value="11">Hungary</option>
	<option value="56">Iceland</option>
	<option value="41">India</option>
	<option value="32">Indonesia</option>
	<option value="53">Ireland</option>
	<option value="16">Israel</option>
	<option value="3">Italy</option>
	<option value="45">Malaysia</option>
	<option value="21">Malta</option>
	<option value="35">Mexico</option>
	<option value="31">Morroco</option>
	<option value="4">Netherlands</option>
	<option value="39">New Zealand</option>
	<option value="23">Norway</option>
	<option value="22">Poland</option>
	<option value="12">Portugal</option>
	<option value="47">Russia</option>
	<option value="28">Serbia</option>
	<option value="49">Singapore</option>
	<option value="36">South Africa</option>
	<option value="1">Spain</option>
	<option value="46">Sri Lanka</option>
	<option value="17">Sweden</option>
	<option value="51">Switzerland</option>
	<option value="48">Thailand</option>
	<option value="7">Turkey</option>
	<option value="6">UK</option>
	<option value="50">Ukraine</option>
	<option value="43">Uruguay</option>
	<option value="25">USA</option>
</select>

<select name="city_id" id="city_id">
	<option value="162">Buenos Aires</option>
	<option value="156">Mendoza</option>
</select>
```

### JavaScript initialization
```javascript
window.addEvent('domready', function() {
	new SelectDependency('city_id', 'country_id', {
		url: 'index.php',
		requestValueKey: 'country_id',
		requestParams: {
			task: 'getCitiesAjax',
		},
		responseLabelKey: 'city_name',
		responseValueKey: 'id'
	});
});
```

### Expected response from server
```json
[{"id":"22","country_id":"10","city_name":"Brussels"},{"id":"130","country_id":"10","city_name":"Gent"}]
```
