# Test-fullCalendar-withAngularjs
TestFullcalendar

<div class="modal  fade" id="meetingForm" tabindex="-1" role="dialog" data-keyboard="false" data-backdrop="static" aria-labelledby="myModalLabeltest" aria-hidden="true">
    <div class="modal-dialog" style="width:90%;height:100%; ">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" click="closeMeetingForm()" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                <h6>会议详情</h6>
            </div>
            <div class="create" style="padding:25px; padding-bottom: 5px;">
                <form class="form-horizontal">
                    <div class="form-group">
                        <label class="control-label col-lg-2" for="email">会议标题:</label>
                        <div class="col-lg-6">
                            <input type="text" class="form-control" id="title" placeholder="会议标题" ng-model="meeting.title">
                        </div>
                    </div>
                    <div class="form-group">
                        <label class="control-label col-lg-2"> </label>
                        <div class="col-lg-3">
                            <label><input type="checkbox" ng-checked="meetingType=='Regular'" ng-click="changeMeetingType()">&nbsp;&nbsp;定期例会</label>
                        </div>
                        <div>
                            <div ng-show="meetingType=='Regular'">
                            </div>
                        </div>
                    </div>
                    <div class="form-group" ng-show="meetingType=='Regular'">
                        <label class="control-label col-lg-2"> </label>
                        <div class="col-lg-4">

                            <label class="radio-inline"><input type="radio" name="optradio" checked>每周</label>
                            <label class="radio-inline"><input type="radio" name="optradio">每两周</label>
                            <label class="radio-inline"><input type="radio" name="optradio">每月</label>
                        </div>
                    </div>
                    <div ng-show="meetingType=='NotRegular'">
                        <div class="form-group">
                            <label class="control-label col-lg-2" for="pwd">会议时间:</label>
                            <div class="col-lg-6">
                                <input type="text" ng-model="notRegularStartDate" mydatepicker />
                                <select ng-model="notRegularStartTime" style="margin-top:10px;">
                                    <option ng-repeat="x in timeslots" value="{{x.value}}">{{x.label}}</option>
                                </select>
                                <select ng-model="notRegularEndTime" style="margin-top:10px;">
                                    <option ng-repeat="x in timeslots" value="{{x.value}}">{{x.label}}</option>
                                </select>
                            </div>
                        </div>
                    </div>
                    <div ng-show="meetingType=='Regular'">
                        <div class="form-group">
                            <label class="control-label col-lg-2" for="pwd">日期范围:</label>
                            <div class="col-lg-6">
                                <input type="text" ng-model="regularStartDate" mydatepicker />
                                <input type="text" ng-model="regularEndDate" mydatepicker />
                                <label class="control-label" for="pwd">&nbsp;&nbsp;&nbsp;时间范围:</label>
                                <select ng-model="regularStartTime" style="margin-top:10px;">
                                    <option ng-repeat="x in timeslots" value="{{x.value}}">{{x.label}}</option>
                                </select>
                                <select ng-model="regularEndTime" style="margin-top:10px;">
                                    <option ng-repeat="x in timeslots" value="{{x.value}}">{{x.label}}</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <div class="form-group">
                        <label class="control-label col-lg-2" for="email">会议地点:</label>
                        <div class="col-lg-2">
                            <angucomplete-alt id="ex1" focus-in="focusIn()" focus-out="focusOut()" placeholder="Search names" pause="100" selected-object="selectedRoomForMeeting" local-data="locationsRooms" search-fields="name" title-field="name" minlength="0" input-class="form-control form-control-small" clear-selected="true">
                            </angucomplete-alt>
                        </div>
                        <span ng-repeat="tempRoom in selectedRooms">&nbsp;&nbsp;<label class="badge">{{tempRoom.name}}</label>&nbsp;&nbsp;<a href="" ng-click="removeFromSelectedRooms(tempRoom)"><i class="fa fa-remove" style="margin-top:3px;"></i></a></span>
                    </div>

                    <div class="form-group">
                        <label class="control-label col-lg-2">会议内容:</label>
                        <div class="col-lg-8">
                            <textarea class="form-control" id="exampleFormControlTextarea1" ng-model="meeting.content" rows="5" placeholder="会议内容"></textarea>
                        </div>
                    </div>
                    <div class="form-group">
                        <label class="control-label col-lg-2">附件:</label>
                        <div class="col-lg-8">
                            <a href="" class="btn btn-sm btn-default   pull-left" style="margin-top:5px; font-size:14px;" ngf-select="uploadDocs($files)" multiple accept="*/*" ngf-max-size="20MB">
                                <i class="fa fa-paperclip" aria-hidden="true"></i>&nbsp;附件({{files.length}}个)
                            </a>
                            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                            <a ng-repeat="tempDoc in uploadedFiles" href="" style="margin-top:7px;"><i class="fa fa-file" style="margin-right:5px; margin-top:5px;"></i>{{tempDoc.fileName}}&nbsp;&nbsp;&nbsp;&nbsp;</a>
                        </div>
                    </div>
                    <div class="form-group">
                        <label class="control-label col-lg-2">参会人:</label>
                        <div class="col-lg-2">
                            <div angucomplete-alt id="search_specified_users" placeholder="输入用户名" pause="500" selected-object="selectedUserForMeeting" remote-url="/api/linkones/gateway/search/users?searchstr=" remote-url-data-field="data" title-field="username" minlength="3" input-class="form-control form-control-small" match-class="highlight" clear-selected="true">
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-lg-2"></label>
                            <div class="col-lg-8">

                                <div id="chat-block" style="margin-left:-25px;margin-top:10px;">

                                    <ul class="online-users list-inline">

                                        <li ng-repeat="tempUser in requiredUsers">
                                            <a href="" ng-click="changeToOptional(tempUser)"><img src="http://placehold.it/300x300" alt="user" style="width:80px;height:80px" class="img-responsive profile-photo img-circle" /><span ng-show="organizer.id != tempUser.id" style="font-size:12px;position: absolute;margin-top:80px;margin-left:15px; ">Required</span></a><a href="" ng-click="removeMeetingUserFromRequiredUsers(tempUser)" ng-show="organizer.id != tempUser.id"><i class="fa fa-remove"></i></a>
                                        </li>

                                        <li ng-repeat="tempUser in optionalUsers">
                                            <a href="" ng-click="changeToRequired(tempUser)"><img src="http://placehold.it/300x300" alt="user" style="width:80px;height:80px" class="img-responsive profile-photo img-circle" /><span style="font-size:12px;position: absolute;margin-top:80px;margin-left:18px;">Optional</span></a>
                                            <a href="" ng-click="removeMeetingUserFromOptionalUsers(tempUser)"><i class="fa fa-remove"></i></a></li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <!--
                            <div class="form-group">
                                <label class="control-label col-lg-2" for="email">是否参加:</label>
                                <div class="col-lg-2">
                                    <select class="form-control" id="sel1">
                                        <option>确定参加</option>
                                        <option>不参加</option>
                                        <option>暂时待定</option>
                                    </select>
                                </div>
                            </div>
                        -->
                    </div>
                </form>
                <hr />
                <div style="text-align: center">
                    <a href="" ng-click="createMeeting()" class="btn btn-default btn-circle" style="width:200px;">&nbsp;&nbsp;保&nbsp;&nbsp;&nbsp;&nbsp;存&nbsp;&nbsp;</a>
                    <a href="" ng-click="closeMeetingForm()" class="btn btn-default btn-circle" style="width:200px;">&nbsp;&nbsp;关&nbsp;&nbsp;&nbsp;&nbsp;闭&nbsp;&nbsp;</a>
                </div>
                <br>
                <br>
                <br>
            </div>
        </div>
    </div>
</div>





<div class="card ">
    <div class="card-header ">
        <!--        <h5 class="card-title">日程安排</h5>-->
        <!--        <p class="card-category" style=" color: #9A9A9A; margin-top: -15px;">24 Hours performance</p> -->
    </div>
    <div class="card-body ">
        <div class="calendar" ng-model="eventSources" calendar="myCalendar1" ui-calendar="uiConfig.calendar" style="margin-bottom: 5px;" id="calendarView"></div>


        <div id="resourceView" ng-show="resourceView==true">
          
        <div class="col-sm-10">
            <select name="study" id="study-selector" class="form-control shortselector">
                <option value="1">Eco</option>
                <option value="2">TAC</option>
                <option value="3">RMN</option>
            </select>
        </div>
        <div id="calendar"></div>

        <div class="modal fade" id="newAppointment" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <div class="modal-body">
                            <h4>Form</h4>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        </div>
    </div>
    <div class="card-footer">
        <hr>
        <div class="stats" style=" color: #9A9A9A;"> <i class="fa fa-calendar"></i> 日程安排 </div>
    </div>
</div>
