var prefix = '/statistic/compliance';
var suffix = '/statistic/averageCompare';
// 日期时间选择器
layui.use('laydate', function() {
    var laydate = layui.laydate;
    laydate.render({
        elem : '#startDate',
        format : 'yyyy-MM-dd',
        value : preMonth(preDay(new Date()))
    });
}) .use('laydate', function() {
    var laydate = layui.laydate;
    laydate.render({
        elem : '#endDate',
        format : 'yyyy-MM-dd',
        value : preDay(new Date())
    });
});
// 前一天
function preDay(nowDate) {
    if (nowDate != null) {
        return new Date(nowDate.getTime() - 24 * 60 * 60 * 1000);
    }
}
// 前一个月
function preMonth(nowDate) {
    if (nowDate != null) {
        return new Date(nowDate.setMonth((nowDate.getMonth() - 1)));
    }
}
var siteCodes;
function load(type) {
    showLoad();
    $('#exampleTable').bootstrapTable({
        method : 'get', // 服务器数据的请求方式 get or post
        url : prefix + "/avglist",
        // showRefresh : true,
        // showToggle : true,
        // showColumns : true,
        iconSize : 'outline',
        toolbar : '#exampleToolbar',
        striped : true, // 设置为true会有隔行变色效果
        dataType : "json", // 服务器返回的数据类型
        pagination : true, // 设置为true会在底部显示分页条
        pageSize : 15, // 如果设置了分页，每页数据条数
        pageNumber : 1, // 如果设置了分布，首页页码
        // queryParamsType : "limit",
        // //设置为limit则会发送符合RESTFull格式的参数
        singleSelect : true, // 设置为true将禁止多选
        // contentType : "application/x-www-form-urlencoded",
        // //发送到服务器的数据编码类型
        // search : true, // 是否显示搜索框
        // showColumns : true, // 是否显示内容下拉框（选择显示的列）
        sidePagination : "server", // 设置在哪里进行分页，可选值为"client" 或者 "server"
        queryParams : function(params) {
            return {
                pageSize : params.limit,
                pageNumber : (params.offset / params.limit) + 1,
                startDate : $("#startDate").val(),
                endDate : $("#endDate").val(),
                siteCodes : $.siteTree.siteCodes()?$.siteTree.siteCodes().join():undefined,
                type:type
            };
        },onLoadSuccess: function(){  //加载成功时执行
            closeLoad();
        },
        columns : [ [ {
            field : 'siteName',
            title : '站点名称',
            align : 'center',
            width: '124px',
            valign : 'middle',
            colspan : 1,
            rowspan : 2
        }, {
            title : 'PM<sub>2.5</sub>（μg/m³）',
            width: '360px',
            align : 'center',
            valign : 'middle',
            colspan : 4,
            rowsapn : 1
        }, {
            title : 'PM<sub>10</sub>（μg/m³）',
            width: '360px',
            align : 'center',
            valign : 'middle',
            colspan : 4,
            rowsapn : 1
        }, {
            title : 'O<sub>3</sub>-8h（μg/m³）',
            width: '360px',
            align : 'center',
            valign : 'middle',
            colspan : 4,
            rowsapn : 1
        },{
            field : 'sumDays',
            title : '有效监测天数',
            align : 'center',
            width: '124px',
            valign : 'middle',
            colspan : 1,
            rowspan : 2
        } ,{
            field : 'pressValiddays',
            title : '综合达标天数',
            align : 'center',
            width: '124px',
            valign : 'middle',
            colspan : 1,
            rowspan : 2
        }, {
            field : 'wsOverproofdays',
            title : '综合达标率',
            align : 'center',
            width: '124px',
            valign : 'middle',
            colspan : 1,
            rowspan : 2,
            formatter: function (value,row,index) {
                return value+"%"
            }
        }], [
            {
                field : 'pm25Overproofdays',
                title : '实际达标天数',
                align : 'center',
                valign : 'middle'
            }, {
                field : '',
                title : '无效',
                align : 'center',
                valign : 'middle'
            }, {
                field : 'pm25Validdays',
                title : '无效天数',
                align : 'center',
                valign : 'middle'
            }, {
                field : 'wdAvg',
                title : '达标率',
                align : 'center',
                valign : 'middle',
                formatter: function (value,row,index) {
                    return value+"%"
                }
            },{
            field : 'pm10Overproofdays',
            title : '实际达标天数',
            align : 'center',
            valign : 'middle'
        }, {
            field : '',
            title : '无效',
            align : 'center',
            valign : 'middle'
        }, {
            field : 'pm10Validdays',
            title : '无效天数',
            align : 'center',
            valign : 'middle'
        }, {
            field : 'wsAvg',
            title : '达标率',
            align : 'center',
            valign : 'middle',
            formatter: function (value,row,index) {
                return value+"%"
            }
        },{
            field : 'o3eightOverproofdays',
            title : '实际达标天数',
            align : 'center',
            valign : 'middle'
        }, {
            field : '',
            title : '无效',
            align : 'center',
            valign : 'middle'
        }, {
            field : 'o3eightValiddays',
            title : '无效天数',
            align : 'center',
            valign : 'middle'
        }, {
            field : 'humiAvg',
            title : '达标率',
            align : 'center',
            valign : 'middle',
            formatter: function (value,row,index) {
                return value+"%"
            }
        }] ]
    });
}

function reload() {
    siteCodes = $.siteTree.siteCodes();
    if (siteCodes.length == 0){
        layer.msg('未选择站点');
        return;
    }
    var type = $("input[name='dataType']:checked").val();
    var examineType = $("input[name='examineType']:checked").val();
    siteCodes = siteCodes.join();
    $('#exampleTable').bootstrapTable('destroy');
    load(type,examineType);
}


var loadIndex = void 0;
function showLoad() {
    loadIndex = layer.msg('请稍后...', {icon: 16, shade: [0.5, '#f5f5f5'], scrollbar: false, offset: 'auto', time: 30000});
}

function closeLoad() {
    layer.close(loadIndex);
}
// 导出Excel
function exportExcel() {
    var type = $("input[name='dataType']:checked").val();
    var examineType = $("input[name='examineType']:checked").val();
    layer.confirm('确定要导出当前记录？', {
        btn : [ '确定', '取消' ]
    }, function(index) {
        layer.close(index);
        var url = "";
        url += prefix + "/avgExportExcel?startDate=" + $("#startDate").val()
            + "&endDate=" + $("#endDate").val() + "&siteCodes="
            + (siteCodes ? siteCodes : "") +"&type="+type+"&examineType="+examineType;
        window.location.href = url
    })
}