# Sample Transaction Model
class CompanyAccount(models.Model):
    company = models.OneToOneField(Company, on_delete=models.PROTECT)
    balance = models.DecimalField(max_digits=15, decimal_places=2)
    last_updated = models.DateTimeField(auto_now=True)

class LedgerEntry(models.Model):
    sender = models.ForeignKey(CompanyAccount, related_name='debits')
    receiver = models.ForeignKey(CompanyAccount, related_name='credits')
    amount = models.DecimalField(max_digits=12, decimal_places=2)
    timestamp = models.DateTimeField(auto_now_add=True)
    reference = models.CharField(max_length=255)
    status = models.CharField(max_length=20, choices=TRANSACTION_STATES)
