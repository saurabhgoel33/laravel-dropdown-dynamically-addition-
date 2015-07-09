# laravel-dropdown-dynamically-addition-
addition of rows dynamically
<script type="text/javascript">
        var count = 1;
   
    $(document).ready(function() {           
             $(".CHAPTER_ID").hide();
             $(".CHAPTER_DESC").hide();
             $(".ASS_VALUE").hide();
        $(".radio-inline1").click(function(){
                $(".CHAPTER_ID").show();
                $(".CHAPTER_DESC").show();
                $(".ASS_VALUE").show();
            });  
            $(".radio-inline").click(function(){
            $(".CHAPTER_ID").hide();
            $(".CHAPTER_DESC").hide();
            $(".ASS_VALUE").hide();
            }); 
        
            autofill();    		 
	});
        
         function addrow() {
           count++;
        //  alert($('#count').val());
        $(".remove").parent().remove();
        var tr = "<tr >" + "<td><input type='checkbox' id='CHECKED' name='CHECKED' class=' CHECKED' /></td>"+
               "<td><select class='form-control WAREHOUSE_ID' id='WAREHOUSE_ID" + count + "'><option value='0' >--Select--</option>@foreach($WAREHOUSE_ID as $key=>$value)<option value={{$key}} >{{$value}}</option>@endforeach</select></td>" +

                "<td><input type='text' name='WAREHOUSE_CODE' id='WAREHOUSE_CODE' class='form-control WAREHOUSE_CODE" + count + "' ></td>" +
               "<td><input type='checkbox' id='CHECKED' name='CHECKED' class='CHECKED' ></td>"+
                //  "<td> <div class='input-append date date-picker' > <input class='DOB' readonly size='16' type='text' name='DOB' id='DOB" + count + "' ><span class='add-on' style='width: 11px;height: 11px'><i class='icon-calendar'></i></span>  </div></td>" +
              
                "<td><input type='text' name='CURRENT_STOCK' class='form-control CURRENT_STOCK' id='CURRENT_STOCK" + count + "' ></td>" +
                "<td><input type='text' name='COMMITED' class='form-control COMMITED' id='COMMITED" + count + "' ></td>" +
                "<td><input type='text' name='ORDERED' class='form-control ORDERED' id='ORDERED" + count + "' ></td>" +
                "<td><input type='text' name='AVAILABLE' class='form-control AVAILABLE' id='AVAILABLE" + count + "' ></td>" +
                "<td><input type='text' name='MIN_WARE' class='form-control MIN_WARE' id='MIN_WARE" + count + "' ></td>" +
                "<td><input type='text' name='MAX_WARE' class='form-control MAX_WARE' id='MAX_WARE" + count + "' ></td>" +
               
                "<td><input type='button' class='btn btn-primary' value='+' onclick='addrow()'></td>" +
                "<td><input type='button' class='btn  btn-danger' value='-' onclick='removerow(this)'></td>" +
                "</tr>";
        // alert(tr);
       
        $("#scott").append(tr);
        var a = parseInt($('#count').val()) + 1;
        document.getElementById('count').value = a;
       
    var ddlArray= new Array();
    var ddl = document.getElementById('WAREHOUSE_ID');
    
for (i = 0; i < ddl.options.length; i++) {
   ddlArray[i] = ddl .options[i].value; 
}
        var selected=new Array();
            $('.WAREHOUSE_ID option:selected').each(function() {
                selected.push($(this).val());
            });
            var foo = [];
var i = 0;
jQuery.grep(ddlArray, function(el) {

    if (jQuery.inArray(el, selected) == -1) foo.push(el);
    i++;
});

    alert(" the difference is " + foo);
    
     for(  i=0;i<=selected.length;i++)
     $('#WAREHOUSE_ID'+count).find('option[value='+selected[i]+']').remove();
    for(  i=0;i<=foo.length;i++)
       {        
        $('#WAREHOUSE_ID'+count).find('option[value='+foo[i]+']').appendTo('#WAREHOUSE_ID'+count);
      }  
     
      
        $(".WAREHOUSE_ID").change(function() {
            $.ajax({
                    // Change the link to the file you are using
                    url: '{{URL::to('/item_master/crea')}}',
                    type: 'post',
                    // This just sends the value of the dropdown
                    data: { client: $(this).val() },
                    success: function(response) {
                        // Parse the jSON that is returned
                        // Using conditions here would probably apply
                        // incase nothing is returned
                        
                      //  var Vals    =   JSON.parse(response.item);
                        var data = response.item;

for(var i in data)
{
     var id = data[i].WAREHOUSE_NAME;
 
     
}
  
                        // These are the inputs that will populate
                        $('.WAREHOUSE_CODE'+count).val(id);
                        
                    }
            });
        });        
       
       
     
    }
    function autofill()
    {
           $(".WAREHOUSE_ID").change(function() {
            $.ajax({
                    // Change the link to the file you are using
                    url: '{{URL::to('/item_master/crea')}}',
                    type: 'post',
                    // This just sends the value of the dropdown
                    data: { client: $(this).val() },
                    success: function(response) {
                        // Parse the jSON that is returned
                        // Using conditions here would probably apply
                        // incase nothing is returned
                        
                      //  var Vals    =   JSON.parse(response.item);
                        var data = response.item;

for(var i in data)
{
     var id = data[i].WAREHOUSE_NAME;
  
     
}
                     
                        // These are the inputs that will populate
                        $('.WAREHOUSE_CODE').val(id);
                        
                    }
            });
        });
    }
   
    function removerow(row)
    {
        $(row).parent().parent().remove();
        count--;
    }
    
	</script>
