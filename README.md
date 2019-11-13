# 看一下
```
   // 1.删除自己本身带有的职位
        CompanyDTO companyDTO = adminLimitService.selectAllowLoginCompanyInfo();
        CompanyUser companyUser = new CompanyUser();
        companyUser.setUserNumber(modifyPositionVO.getUserNumber());
        companyUser.setCompanyPId(companyDTO.getId());
        List<CompanyUser> companyUserList = companyUserMapper.select(companyUser);
        for (CompanyUser user : companyUserList){

            companyUserMapper.deleteByPrimaryKey(user.getId());
        }


        // 获得勾选的对象
        List<CompanyTreeDTO> positionDataList = modifyPositionVO.getPositionData();

        List<Integer> intList = new ArrayList<>();
        // 获得勾选的节点
        for (CompanyTreeDTO companyTreeDTO : positionDataList){
            if (companyTreeDTO.getChecked()){
                intList.add(companyTreeDTO.getId());
            }

            /*if (companyTreeDTO.getIndeterminate() || ObjectUtils.isNotEmpty(companyTreeDTO.getIndeterminate())){
                intList.addAll(getCompanyNodeId(companyTreeDTO.getChildren()));
            }*/
        }

        Integer count = null;
        for (Integer companyId : intList){

            CompanyUser orgUser = new CompanyUser();
            orgUser.setCompanyPId(companyDTO.getId());
            orgUser.setCompanyId(companyId);
            orgUser.setUserNumber(modifyPositionVO.getUserNumber());
            orgUser.setUserName(modifyPositionVO.getUserName());
            orgUser.setIsEnabled(1);
            orgUser.setWorkNo(modifyPositionVO.getWorkNo());
            orgUser.setCreateTime(new Date());
            orgUser.setUpdateTime(new Date());

            count = companyUserMapper.insertSelective(orgUser);
        }

```
