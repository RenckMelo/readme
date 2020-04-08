# readme
Segunda etapa Supera


<!DOCTYPE html>
<html>
 <head>

<style>
    body > table{
    width: 80%;
}

table{
    border-collapse: collapse;
}
table.list{
    width:100%;
}

td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
}
tr:nth-child(even),table.list thead>tr {
    background-color: #dddddd;
}

input[type=text], input[type=number] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

input[type=submit]{
    width: 30%;
    background-color: #ddd;
    color: #000;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

form div.form-action-buttons{
    text-align: right;
}

a{
    cursor: pointer;
    text-decoration: underline;
    color: #0000ee;
    margin-right: 4px;
}

label.validation-error{
    color:   red;
    margin-left: 5px;
}

.hide{
    display:none;
</style>

</head>

	<body> 
		<table>
			<tr>

				<td>
					<form onsubmit="event.preventDefault();onFormSubmit()" autocomplete="off" >
						<div>
						   <label>Nome Completo</label>
						   <input type="text" name="nomecomp" id="nomecomp">
                        </div>

                        <div>
						   <label>Codigo Do Empregado</label>
						   <input type="text" name="codemp" id="codemp">
                        </div>

                        <div>
						   <label>Salario</label>
						   <input type="text" name="sal" id="sal">
                        </div>

                        <div>
						   <label>Cidade</label>
						   <input type="text" name="cid" id="cid">
                        </div>
                        <div class="form-action-buttons">
                        	<input type="submit" value="Submit">
                        </div>
                    </form>
				</td>
                <td>
                    <table class="list" id="employeeList">
                    	<thead>
                    		<tr>
                    			<th>Nome Completo</th>
                    			<th>Codigo Do Empregado</th>
                    			<th>Salario</th>
                    			<th>Cidade</th>
                    			<th></th>                    			                    					
                    		</tr>
                    	</thead>
                    	<tbody>
                    		
                    	</tbody>
                    </table>
				

				</td>	

            </tr>
		</table>

		<script>
      var selectedRow = null


function  onFormSubmit(){
    var formData = readFormData();
        if (selectedRow == null)
            insertNewRecord(formData);
        else
                updateRecord(formData);
            resetForm();
    
}

function readFormData(){
    var formData = {};
    formData["nomecomp"] = document.getElementById("nomecomp").value;
    formData["codemp"] = document.getElementById("codemp").value;
    formData["sal"] = document.getElementById("sal").value;
    formData["cid"] = document.getElementById("cid").value;
    return formData;

}

function insertNewRecord(data) {

    var table = document.getElementById("employeeList").getElementsByTagName('tbody')[0];

    var newRow = table.insertRow(table.length);

    cell1 = newRow.insertCell(0);
    cell1.innerHTML = data.nomecomp;

    cell2 = newRow.insertCell(1);
    cell2.innerHTML = data.codemp;

    cell3 = newRow.insertCell(2);
    cell3.innerHTML = data.sal;

    cell4 = newRow.insertCell(3);
    cell4.innerHTML = data.cid;

    cell4 = newRow.insertCell(4);
    cell4.innerHTML = `<a onClick= "onEdit(this)">Editar</a> 
                       <a onClick="onDelete(this)">Deletar</a >`;



}
function resetForm(){
document.getElementById("nomecomp").value=" ";
document.getElementById("codemp").value=" ";
document.getElementById("sal").value=" ";
document.getElementById("cid").value=" ";
selectedRow = null;


}

function onEdit(td){
    selectedRow = td.parentElement.parentElement;
    document.getElementById("nomecomp").value = selectedRow.cells[0].innerHTML;
    document.getElementById("codemp").value = selectedRow.cells[1].innerHTML;
    document.getElementById("sal").value = selectedRow.cells[2].innerHTML;
    document.getElementById("cid").value = selectedRow.cells[3].innerHTML;
} 

function updateRecord(formData) {
    selectedRow.cells[0].innerHTML = formData.nomecomp;
    selectedRow.cells[1].innerHTML = formData.codemp;
    selectedRow.cells[2].innerHTML = formData.sal;
    selectedRow.cells[3].innerHTML = formData.cid;
}

function onDelete(td){
    if (confirm('deletar?')) {
        row = td.parentElement.parentElement;
        document.getElementById("employeeList").deleteRow(row.rowIndex);
        resetForm();
    }
}

      
        </script>
	</body>
</html>
