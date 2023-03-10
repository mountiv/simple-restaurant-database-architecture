# Solution of Database Architecture using RMDBS

<h3 align="center">Basic tables</h3>

<div align="center">
	<table>
		<tr>
			<th>No</th>
			<th>table name</th>
			<th>fields</th>
			<th>description</th>  
		</tr>
		<tr>
			<th>1</th>
			<td>users</td>
			<td>id, name, email, phone</td>
			<td>basic information of users are saved in this table.</td>  
		</tr>
		<tr>
			<th>2</th>
			<td>user_section_relations</td>
			<td>id, user_id, section_id</td>
			<td>if user is enter the special section of stadium, user_id and section_id is saved in this table.</td>  
		</tr>
		<tr>
			<th>3</th>
			<td>food_stations</td>
			<td>id, fst_name</td>
			<td>this is food station table, simply include only food station information.</td>  
		</tr>
		<tr>
			<th>4</th>
			<td>sections</td>
			<td>id, sectioin_name</td>
			<td>section data is saved in this table.</td>  
		</tr>
		<tr>
			<th>5</th>
			<td>section_fst_relations</td>
			<td>id, section_id, fst_id</td>
			<td>the relation between section_id and fst_id is saved in this table. "fst" stands for "food station".</td>  
		</tr>
	</table>
</div>
<br/>
<br/>

### MySQL Query

```
SELECT * FROM `food_stations`
	LEFTJOIN `section_fst_relations` WHERE `section_fst_relations`.`fst_id` = `food_stations`.`id`
	LEFTJOIN `sections` WHERE `sections`.`id` = `section_fst_relations`.`section_id`
	LEFTJOIN `user_section_relations` WHERE `user_section_relations`.`user_id` = `users`.`id`
	WHERE `users`.`id` = "CURRENT_USER_ID"
```

<br/>

<p>Backend receives CURRENT_USER_ID from frontend. This means this query is trigged only CURRENT_USER_ID. From CURRENT_USER_ID, we can know what section user is on. From SECTION_ID, we can know what food stations in this sections.</p>
<p>"user_section_relations", "section_fst_relations" are intermediary tables. These tables are made based on my best practice.</p>

