Classroom Automation.
==========================================
**Step 1:**
- open [Google Script](https://script.google.com/) Dashboard
- Click on New Project.
- Add Classroom service to your Project.

![Service Adding](/assesets/Service_Adding.gif)

**Step 2:**
- Remove myfunction() and paste the following code 

```
 function myFunction() {
  MatrialCopier(692017107237) 
 }
 var lst =[]
 function MatrialCopier(CourseId){
  Logger.log("Copying All Files from Classroom to Drive.....")
  var Std=Classroom.Courses.Announcements.list(CourseId);
  var folder = DriveApp.createFolder("Python JRP Batch @ 4:00 PM | Mr.Senapathi >[19th Aug]")
  for(var i =0;i<Std.announcements.length;i++){
    if (Std.announcements[i].hasOwnProperty('materials') && Std.announcements[i].creatorUserId=='114175851596834583774') // creatorUserId is Sir's UserId
    {
      if(lst.includes(Std.announcements[i].updateTime.slice(0,10))){}
      else{
        var NewFolder = folder.createFolder(Std.announcements[i].updateTime.slice(0,10))
        lst.push(Std.announcements[i].updateTime.slice(0,10));
       /*  Logger.log(Std.announcements[i].updateTime.slice(0,10)) */
      }
      for (var j =0;j<Std.announcements[i].materials.length;j++){
        /* Logger.log(Std.announcements[i].materials[j].driveFile.driveFile.title);
        Logger.log(Std.announcements[i].materials[j].driveFile.driveFile.alternateLink); */
        var u =DriveApp.getFileById(Std.announcements[i].materials[j].driveFile.driveFile.alternateLink.split('/')[5])
        u.makeCopy(NewFolder).setName(Std.announcements[i].materials[j].driveFile.driveFile.title)
    }
    }
   }
     var k = '';
   for(var i= 0;i<Std.announcements.length;i++){
    if ( Std.announcements[i].creatorUserId=='114175851596834583774'){
    k=k+'\n\n'+Std.announcements[i].updateTime+'\n\n'+Std.announcements[i].text ;
    }
  }
  folder.createFile('Day_wise_Anouncement.txt',k)
  Logger.log("All Files Copied Successfully.......")
  Logger.log("Access Link  :"+folder.getUrl())
 }
```
**Step 3:**
- Click on run Button.
- Click on Review Permission

![Review Permission](/assesets/Review_permission.png)

- Select the mail through which you are in classroom.

![Mail Selection](/assesets/Select_mail.png)

- click on Advanced Setting below.

![Advansed settings](/assesets/Advanced_settings.png)

- click on Trust user and continue.

![Trust user](/assesets/Trust_user.png)

- Finally scroll Down and Click on allow.

![ Allow Permission ](/assesets/Click_Allow.png)

- Wait untill the code gets completely executed This will copy all the file's,Announcements in google classroom to your Google drive Creatting Day wise folders in it.
- The final Output will crete  folder named "Python JRP Batch @ 4:00 PM | Mr.Senapathi [19th Aug]"
