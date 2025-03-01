/*
 * Copyright (C) 2017-2021
 * All rights reserved, Designed By 深圳中科鑫智科技有限公司
 * Copyright authorization contact 18814114118
 */
package com.shop.cereshop.admin.controller;

import com.shop.cereshop.admin.annotation.NoRepeatSubmit;
import com.shop.cereshop.admin.annotation.NoRepeatWebLog;
import com.shop.cereshop.admin.page.buyer.BuyerUser;
import com.shop.cereshop.admin.page.buyer.BuyerUserDetail;
import com.shop.cereshop.admin.page.buyer.BuyerUserExportDTO;
import com.shop.cereshop.admin.param.buyer.*;
import com.shop.cereshop.admin.param.credit.UpdateCreditParam;
import com.shop.cereshop.admin.param.user.UserSearchParam;
import com.shop.cereshop.admin.service.buyer.CereBuyerUserService;
import com.shop.cereshop.admin.service.channel.ChannelService;
import com.shop.cereshop.commons.constant.IntegerEnum;
import com.shop.cereshop.commons.domain.buyer.CereBuyerUser;
import com.shop.cereshop.commons.domain.channel.Channel;
import com.shop.cereshop.commons.domain.common.Page;
import com.shop.cereshop.commons.domain.label.CerePlatformLabel;
import com.shop.cereshop.commons.domain.user.CerePlatformUser;
import com.shop.cereshop.commons.exception.CoBusinessException;
import com.shop.cereshop.commons.poi.export.ExcelExportUtils;
import com.shop.cereshop.commons.result.Result;
import com.shop.cereshop.commons.utils.GsonUtil;
import io.swagger.annotations.Api;
import io.swagger.annotations.ApiOperation;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.collections4.CollectionUtils;
import org.apache.commons.lang.StringUtils;
import org.springframework.beans.BeanUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

/**
 * 客户管理
 */
@RestController
@RequestMapping("buyer")
/**
 * 注解方式生成日志对象，指定topic生成对象类名
 */
@Slf4j(topic = "BuyerUserController")
@Api(value = "客户管理模块", tags = "客户管理模块")
public class BuyerUserController {

    @Autowired
    private CereBuyerUserService cereBuyerUserService;

    @Autowired
    private ChannelService channelService;

    /**
     * 客户管理查询
     * @param param
     * @return
     */
    @PostMapping(value = "getAll")
    @ApiOperation(value = "客户管理查询")
    public Result<Page<BuyerUser>> getAll(@RequestBody BuyerGetAllParam param) throws CoBusinessException{
        Page page=cereBuyerUserService.getAll(param);
        return new Result(page);
    }

    /**
     * 客户详情查询
     * @param param
     * @return
     */
    @PostMapping(value = "getById")
    @ApiOperation(value = "客户详情查询")
    public Result<BuyerUserDetail> getById(@RequestBody BuyerGetByIdParam param) throws CoBusinessException{
        BuyerUserDetail detail=cereBuyerUserService.getById(param);
        return new Result(detail);
    }

    /**
     * 客户绑定标签查询
     * @param param
     * @return
     */
    @PostMapping(value = "getUserLabels")
    @ApiOperation(value = "客户绑定标签查询")
    public Result<List<CerePlatformLabel>> getUserLabels(@RequestBody BuyerGetLabelsParam param) throws CoBusinessException{
        List<CerePlatformLabel> list=cereBuyerUserService.getUserLabels(param);
        return new Result(list);
    }

    /**
     * 标签查询
     * @param param
     * @return
     */
    @PostMapping(value = "getLabels")
    @ApiOperation(value = "标签查询")
    public Result<List<CerePlatformLabel>> getLabels(@RequestBody BuyerGetLabelsParam param) throws CoBusinessException{
        List<CerePlatformLabel> list=cereBuyerUserService.getLabels(param);
        return new Result(list);
    }

    /**
     * 贴标签
     * @param param
     * @return
     */
    @PostMapping(value = "saveUserLabel")
    @NoRepeatSubmit
    @ApiOperation(value = "贴标签")
    @NoRepeatWebLog
    public Result saveUserLabel(@RequestBody BuyerSaveUserLabelParam param,
                                HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformUser user = (CerePlatformUser) request.getAttribute("user");
        cereBuyerUserService.saveUserLabel(param,user);
        return new Result(user.getUsername(),"贴标签", GsonUtil.objectToGson(param));
    }

    /**
     * 加入或取消黑名单
     * @param param
     * @return
     */
    @PostMapping(value = "blacklist")
    @NoRepeatSubmit
    @ApiOperation(value = "加入和取消黑名单")
    @NoRepeatWebLog
    public Result blacklist(@RequestBody BuyerBlackListParam param,
                            HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformUser user = (CerePlatformUser) request.getAttribute("user");
        cereBuyerUserService.blacklist(param,user);
        return new Result(user.getUsername(),"加入或取消黑名单", GsonUtil.objectToGson(param));
    }

    /**
     * 更新积分
     * @param param
     * @return
     */
    @PostMapping(value = "updateCredit")
    @NoRepeatSubmit
    @ApiOperation(value = "更新积分")
    @NoRepeatWebLog
    public Result updateCredit(@RequestBody UpdateCreditParam param,
                            HttpServletRequest request) throws CoBusinessException{
        //获取当前登录账户
        CerePlatformUser user = (CerePlatformUser) request.getAttribute("user");
        cereBuyerUserService.updateCredit(param,user);
        return new Result(user.getUsername(),"更改积分", GsonUtil.objectToGson(param));
    }

    /**
     * 搜索用户信息
     * @param param
     * @return
     */
    @PostMapping(value = "searchUser")
    @NoRepeatSubmit
    @ApiOperation(value = "搜索用户信息")
    @NoRepeatWebLog
    public Result<Page<CereBuyerUser>> searchUser(@RequestBody UserSearchParam param) {
        Page<CereBuyerUser> page = cereBuyerUserService.searchUser(param);
        return new Result(page);
    }

    @PostMapping(value = "export")
    @ApiOperation(value = "用户列表导出")
    public void export(@RequestBody BuyerGetAllParam param, HttpServletRequest request, HttpServletResponse response) throws CoBusinessException {
        param.setPage(null);
        param.setPageSize(null);
        Page<BuyerUser> page = cereBuyerUserService.getAll(param);
        List<BuyerUserExportDTO> list = new ArrayList<>();
        List<String> channelCodeList = page.getList().stream().filter(obj -> StringUtils.isNotBlank(obj.getChannelCode()))
                .map(BuyerUser::getChannelCode).distinct().collect(Collectors.toList());
        Map<String, String> channelNameMap = new HashMap<>();
        if (CollectionUtils.isNotEmpty(channelCodeList)) {
            List<Channel> channelList = channelService.selectByChannelCodeList(channelCodeList);
            channelNameMap = channelList.stream().collect(Collectors.toMap(Channel::getChannelCode, Channel::getChannelName));
        }
        for (BuyerUser buyerUser:page.getList()) {
            BuyerUserExportDTO dto = new BuyerUserExportDTO();
            BeanUtils.copyProperties(buyerUser, dto);
            IntegerEnum terminalEnum = IntegerEnum.terminalMap.get(buyerUser.getTerminal());
            if (terminalEnum != null) {
                dto.setTerminal(terminalEnum.getName());
            }
            String channelCode = buyerUser.getChannelCode();
            if (channelCode != null) {
                dto.setChannelName(channelNameMap.get(channelCode));
            }
            list.add(dto);
        }
        //定义导出的excel名字
        String excelName = "用户列表";
        ExcelExportUtils.exportExcel(request, response, excelName, list, BuyerUserExportDTO.class);
    }
}
