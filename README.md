# Test-fullCalendar-withAngularjs
TestFullcalendar



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
