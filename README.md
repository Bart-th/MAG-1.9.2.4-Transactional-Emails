<?php $_order = $this->getOrder() ?>
<?php if ($_order): ?>
<table cellspacing="0" cellpadding="0" border="0" width="650" style="border:1px solid #EAEAEA;">
    <thead>
        <tr>
            <th align="left" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><?php echo $this->__('Image') ?></th>
            <th align="left" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><?php echo $this->__('Item') ?></th>
            <th align="left" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><?php echo $this->__('Sku') ?></th>
            <th align="center" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><?php echo $this->__('Qty') ?></th>
            <th align="right" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><?php echo $this->__('Subtotal') ?></th>
        </tr>
    </thead>

    <?php $i=0; foreach ($_order->getAllItems() as $_item): ?>
    <?php if($_item->getParentItem()) continue; else $i++; ?>
    <tbody<?php echo $i%2 ? ' bgcolor="#F6F6F6"' : '' ?>>
        <?php echo $this->getItemHtml($_item) ?>
    </tbody>
    <?php endforeach; ?>

    <tbody>
        <?php echo $this->getChildHtml('order_totals') ?>
    </tbody>
</table>
<?php if ($this->helper('giftmessage/message')->isMessagesAvailable('order', $_order, $_order->getStore()) && $_order->getGiftMessageId()): ?>
    <?php $_giftMessage = $this->helper('giftmessage/message')->getGiftMessage($_order->getGiftMessageId()); ?>
    <?php if ($_giftMessage): ?>
<br />
<table cellspacing="0" cellpadding="0" border="0" width="100%" style="border:1px solid #EAEAEA;">
    <thead>
        <tr>
            <th align="left" bgcolor="#EAEAEA" style="font-size:13px; padding:3px 9px"><strong><?php echo $this->__('Gift Message for this Order') ?></strong></th>
        </tr>
    </thead>

    <tbody>

        <tr>
            <td colspan="4" align="left" style="padding:3px 9px">
            <strong><?php echo $this->__('From:'); ?></strong> <?php echo $this->escapeHtml($_giftMessage->getSender()) ?>
            <br /><strong><?php echo $this->__('To:'); ?></strong> <?php echo $this->escapeHtml($_giftMessage->getRecipient()) ?>
            <br /><strong><?php echo $this->__('Message:'); ?></strong><br /> <?php echo $this->escapeHtml($_giftMessage->getMessage()) ?>
            </td>
        </tr>
    </tbody>
</table>
    <?php endif; ?>
<?php endif; ?>
<?php endif; ?>
