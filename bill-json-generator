<!DOCTYPE html>
<html>
<body>

<h2>Bill Json Generator</h2>

<form id="form">
  <label for="Type">Type</label><br>
  <select id="Type" name="Type" onchange="Update()">
      <option value="Law">Law</option>
      <option value="Bill">Bill</option>
  </select>
  <p></p>
  <label for="Tag">Tag</label><br>
  <select id="Tag" name="Tag" onchange="Update()">
      <option value="RP">RP</option>
      <option value="GOV">GOV</option>
      <option value="JUD">JUD</option>
      <option value="ECO">ECO</option>
      <option value="NER">NER</option>
      <option value="AMN">AMN</option>
      <option value="OTH">OTH</option>
  </select>
  <p></p>
  <label for="Revision">If revision, then this should be the id of the bill that is being revised:</label><br>
  <input type="text" id="Revision" name="Revision" value="" onkeyup="Update()"><br>
  <label for="Time Proposed">Time Proposed:</label><br>
  <input type="text" id="Time Proposed" name="Time Proposed" value="" onkeyup="Update()"><br>
  <label for="Voted Time">Voted Time:</label><br>
  <input type="text" id="Voted Time" name="Voted Time" value="" onkeyup="Update()"><br>
  <label for="Vote ended time">Vote ended time:</label><br>
  <input type="text" id="Vote ended time" name="Vote ended time" value="" onkeyup="Update()"><br>
  <label for="Id">Id:</label><br>
  <input type="text" id="Id" name="Id" value="" onkeyup="Update()"><br>
  <label for="Name">Name:</label><br>
  <input type="text" id="Name" name="Name" value="" onkeyup="Update()"><br>
  <label for="Short Name">Short Name:</label><br>
  <input type="text" id="Short Name" name="Short Name" value="" onkeyup="Update()"><br>
  <label for="ProposerSvid">Proposer Svid:</label><br>
  <input type="text" id="ProposerSvid" name="ProposerSvid" value="" onkeyup="Update()"><br>
  <label for="ProposerName">Proposer Name:</label><br>
  <input type="text" id="ProposerName" name="ProposerName" value="" onkeyup="Update()"><br>
  <label for="AuthorSvid1">Author 1 SVID:</label><br>
  <input type="text" id="AuthorSvid1" name="AuthorSvid1" value="" onkeyup="Update()"><br>
  <label for="AuthorName1">Author 1 Name:</label><br>
  <input type="text" id="AuthorName1" name="AuthorName1" value="" onkeyup="Update()"><br>
  <label for="AuthorSvid2">Author 2 SVID:</label><br>
  <input type="text" id="AuthorSvid2" name="AuthorSvid2" value="" onkeyup="Update()"><br>
  <label for="AuthorName2">Author 2 Name:</label><br>
  <input type="text" id="AuthorName2" name="AuthorName2" value="" onkeyup="Update()"><br>
  <label for="AuthorSvid3">Author 3 SVID:</label><br>
  <input type="text" id="AuthorSvid3" name="AuthorSvid3" value="" onkeyup="Update()"><br>
  <label for="AuthorName3">Author 3 Name:</label><br>
  <input type="text" id="AuthorName3" name="AuthorName3" value="" onkeyup="Update()"><br>
  <div id="senators">

  </div>
  <label for="Content">Content</label><br>
  <textarea id="Content" name="Content" rows="20" cols="100" onkeyup="Update()"></textarea><br/>
  <input type="submit" value="Submit">
</form> 
<p>Output</p>
<pre  id="Output" style="outline: 1px solid #ccc;">

</pre>
</body>
</html>

<script>
    function httpGet(theUrl)
    {
        if (window.XMLHttpRequest)
        {// code for IE7+, Firefox, Chrome, Opera, Safari
            xmlhttp=new XMLHttpRequest();
        }
        else
        {// code for IE6, IE5
            xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
        }
        xmlhttp.onreadystatechange=function()
        {
            if (xmlhttp.readyState==4 && xmlhttp.status==200)
            {
                return xmlhttp.responseText;
            }
        }
        xmlhttp.open("GET", theUrl, false );
        xmlhttp.send();    

        return xmlhttp.response;
    }

    // creates the senator vote things

    content = httpGet("https://raw.githubusercontent.com/Coca162/SpookVooper-Journal/main/CurrentSenators.json")
    data = JSON.parse(content)
    console.log(data)


    div = document.getElementById("senators")
    Senators = data.Senators
    data.Senators.forEach(item => {
        data = `<label for="${item.name}-vote">${item.name}:</label><br>
        <select id="${item.name}-vote" name="${item.name}-vote" onchange="Update()">
            <option value="aye">aye</option>
            <option value="abs">abs</option>
            <option value="nay">nay</option>
        </select><p style="margin-bottom:0px;margin-top:4px;"></p>`
        div.innerHTML += data;
    });




    function Update() {
        form = document.getElementById("form")

        data = {}
        data['Type'] = document.getElementById("Type").value
        data['Tag'] = document.getElementById("Tag").value
        data['Id'] = Number.parseInt(document.getElementById("Id").value)
        data['Name'] = document.getElementById("Name").value
        data['Short Name'] = document.getElementById("Short Name").value
        data['Revision'] = Number.parseInt(document.getElementById("Revision").value)
        data['Vote ended time'] = Number.parseInt(document.getElementById("Vote ended time").value)
        data['Voted Time'] = Number.parseInt(document.getElementById("Voted Time").value)
        data['Time Proposed'] = Number.parseInt(document.getElementById("Time Proposed").value)
        data['Proposer'] = {}
        data['Proposer']['svid'] = document.getElementById("ProposerSvid").value
        data['Proposer']['name'] = document.getElementById("ProposerName").value
        
        // do author stuff

        data['Authors'] = []

        for (i = 1; i < 4; i++) {
            if (document.getElementById(`AuthorSvid${i}`).value == "" && document.getElementById(`AuthorName${i}`).value == "") {
                continue
            }
            d = {}
            d['svid'] = document.getElementById(`AuthorSvid${i}`).value
            d['name'] = document.getElementById(`AuthorName${i}`).value
            data['Authors'].push(d)
        }

        data['Content'] = document.getElementById("Content").value

        // do senators vote
        data['Votes'] = []
        Senators.forEach(item => {
            d = {}
            d['name'] = item.name
            d['svid'] = item.svid
            d['district'] = item.district
            d['vote'] = document.getElementById(`${item.name}-vote`).value
            data['Votes'].push(d)
        })
        document.getElementById("Output").innerHTML = JSON.stringify(data,null, 2)
    }
</script>
